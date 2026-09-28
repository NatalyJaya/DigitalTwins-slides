<script setup lang="ts">
import { onBeforeUnmount, onMounted, ref } from 'vue'
import * as THREE from 'three'
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js'
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js'

const MODEL_URL = `${import.meta.env.BASE_URL}models/heart.glb`
const TARGET_SIZE = 2.0
const MAX_POLL_FRAMES = 600

type Status = 'loading' | 'ready' | 'error'

const container = ref<HTMLDivElement | null>(null)
const status = ref<Status>('loading')

let renderer: THREE.WebGLRenderer | undefined
let scene: THREE.Scene | undefined
let camera: THREE.PerspectiveCamera | undefined
let controls: OrbitControls | undefined
let model: THREE.Object3D | undefined

let animationId = 0
let pollId = 0
let pollFrames = 0
let resizeObserver: ResizeObserver | undefined
let initialized = false
let disposed = false

function measure() {
  const el = container.value
  return { width: el?.clientWidth ?? 0, height: el?.clientHeight ?? 0 }
}

function normalizeModel(object: THREE.Object3D) {
  object.position.set(0, 0, 0)
  object.scale.set(1, 1, 1)
  object.updateMatrixWorld(true)

  const box = new THREE.Box3().setFromObject(object)
  const size = box.getSize(new THREE.Vector3())
  const maxDimension = Math.max(size.x, size.y, size.z) || 1
  object.scale.setScalar(TARGET_SIZE / maxDimension)

  object.updateMatrixWorld(true)
  const centered = new THREE.Box3().setFromObject(object)
  const center = centered.getCenter(new THREE.Vector3())
  object.position.sub(center)
  object.updateMatrixWorld(true)

  object.traverse((child) => {
    if (!(child instanceof THREE.Mesh) || !child.material)
      return
    const materials = Array.isArray(child.material) ? child.material : [child.material]
    for (const material of materials) {
      if ('roughness' in material) material.roughness = 0.4
      if ('metalness' in material) material.metalness = 0.1
      material.side = THREE.DoubleSide
    }
  })
}

function fitCamera() {
  if (!camera || !model)
    return

  const { width, height } = measure()
  if (width && height) {
    camera.aspect = width / height
    camera.updateProjectionMatrix()
  }

  const sphere = new THREE.Box3().setFromObject(model).getBoundingSphere(new THREE.Sphere())
  const radius = Math.max(sphere.radius, 0.0001)

  const vFov = THREE.MathUtils.degToRad(camera.fov)
  const distV = radius / Math.sin(vFov / 2)
  const distH = radius / Math.sin(Math.atan(Math.tan(vFov / 2) * camera.aspect))
  const distance = Math.max(distV, distH) * 1.15

  camera.position.set(sphere.center.x, sphere.center.y, sphere.center.z + distance)
  camera.lookAt(sphere.center)
  controls?.target.copy(sphere.center)
  controls?.update()
}

function loadModel() {
  new GLTFLoader().load(
    MODEL_URL,
    (gltf) => {
      if (disposed)
        return

      const heart = gltf.scene
      normalizeModel(heart)
      scene?.add(heart)
      model = heart

      if (renderer && camera) {
        controls = new OrbitControls(camera, renderer.domElement)
        controls.enableDamping = true
        controls.enableZoom = false
        controls.enablePan = false
        controls.autoRotate = true
        controls.autoRotateSpeed = 1
      }

      fitCamera()
      status.value = 'ready'
    },
    undefined,
    (error) => {
      console.error('[Heart3D] Error loading model:', MODEL_URL, error)
      if (!disposed)
        status.value = 'error'
    }
  )
}

function init() {
  if (initialized || disposed)
    return

  const { width, height } = measure()
  if (!width || !height)
    return

  initialized = true

  try {
    scene = new THREE.Scene()

    camera = new THREE.PerspectiveCamera(45, width / height, 0.1, 100)

    renderer = new THREE.WebGLRenderer({
      antialias: true,
      alpha: true,
    })
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
    renderer.setSize(width, height)
    renderer.setClearColor(0x000000, 0)
    renderer.domElement.style.width = '100%'
    renderer.domElement.style.height = '100%'
    renderer.domElement.style.display = 'block'
    container.value?.appendChild(renderer.domElement)
  }
  catch (error) {
    console.error('[Heart3D] WebGL initialization failed:', error)
    status.value = 'error'
    return
  }

  scene.add(new THREE.AmbientLight(0xffffff, 2.5))

  const key = new THREE.DirectionalLight(0xffffff, 4)
  key.position.set(5, 5, 5)
  scene.add(key)

  const fill = new THREE.DirectionalLight(0xffffff, 2)
  fill.position.set(-5, 2, 3)
  scene.add(fill)

  loadModel()
  animate()
}

function animate() {
  if (disposed)
    return

  animationId = requestAnimationFrame(animate)
  controls?.update()
  if (renderer && scene && camera)
    renderer.render(scene, camera)
}

function resize() {
  if (!renderer || !camera)
    return

  const { width, height } = measure()
  if (!width || !height)
    return

  camera.aspect = width / height
  camera.updateProjectionMatrix()
  renderer.setSize(width, height)

  if (model)
    fitCamera()
}

function startPolling() {
  if (pollId || disposed)
    return

  const tick = () => {
    pollId = 0
    if (disposed)
      return

    init()

    if (initialized || ++pollFrames >= MAX_POLL_FRAMES)
      return

    pollId = requestAnimationFrame(tick)
  }

  pollId = requestAnimationFrame(tick)
}

function dispose() {
  if (disposed)
    return
  disposed = true

  cancelAnimationFrame(animationId)
  cancelAnimationFrame(pollId)
  animationId = 0
  pollId = 0

  resizeObserver?.disconnect()
  resizeObserver = undefined

  controls?.dispose()
  controls = undefined

  if (scene) {
    scene.traverse((child) => {
      if (!(child instanceof THREE.Mesh))
        return
      child.geometry?.dispose()
      const materials = Array.isArray(child.material) ? child.material : [child.material]
      for (const material of materials)
        material.dispose()
    })
  }

  if (renderer) {
    renderer.dispose()
    renderer.forceContextLoss()
  }

  const canvas = renderer?.domElement
  if (canvas && canvas.parentNode === container.value)
    canvas.parentNode.removeChild(canvas)

  scene = undefined
  camera = undefined
  renderer = undefined
  model = undefined
}

onMounted(() => {
  init()
  if (!initialized)
    startPolling()

  resizeObserver = new ResizeObserver(() => {
    if (!initialized) {
      init()
      if (!initialized)
        return
    }
    resize()
  })

  if (container.value)
    resizeObserver.observe(container.value)
})

onBeforeUnmount(dispose)
</script>

<template>
  <div class="w-full h-full min-h-[12rem] relative overflow-hidden">
    <div ref="container" class="absolute inset-0" />
    <div
      v-if="status !== 'ready'"
      class="absolute inset-0 z-10 flex items-center justify-center px-3 text-center text-s"
      :class="status === 'error' ? 'text-red-400' : 'text-white/50'"
    >
      <span v-if="status === 'error'">
        3D model unavailable
      </span>
      <span v-else class="animate-pulse">Loading 3D model…</span>
    </div>
  </div>
</template>
