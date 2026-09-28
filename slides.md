---
theme: '@ktym4a/slidev-theme-ktym4a'
title: Digital Twins
info: |
  Digital Twins - Overview
  Nataly Jaya, Universitat de Lleida
class: text-center
drawings:
  persist: false
transition: slide-left
duration: 35min
---

<!-- ============ COVER ============ -->

<div class="flex flex-col items-center gap-6">
 
   <h1>Digital Twins - Overview</h1>
    <img src="https://placehold.co/400x400?text=Photo" class="w-28 h-28 rounded-full object-cover shadow-xl border-4 border-emerald-500" />
    <p class="opacity-70 text-xl"> Nataly Jaya · UdL</p>
  

</div>

---
layout: section
---

<!-- ============ 01 INTRODUCTION ============ -->

<div class="text-7xl font-800 bg-gradient-to-r from-emerald-500 to-amber-500 bg-clip-text text-transparent leading-none">01</div>

# INTRODUCTION

---
transition: slide-left
---

# From Apollo 13 to Digital Twins

<div class="grid grid-cols-3 gap-6 mt-6">
<div v-click class="text-center transition-all duration-700 transform hover:scale-105"> <div class="text-amber-500 font-bold mb-2">1970</div> <img src="/public/Apolo13-Astronauts.jpg" class="w-full h-56 object-cover rounded-lg shadow-xl border border-white/10" /> <p class="text-sm opacity-60 mt-3"> Fig. 1 · Apollo 13 crew. Source: El Litoral </p> </div>
<div v-click class="text-center transition-all duration-700 transform hover:scale-105"> <div class="text-amber-500 font-bold mb-2">2002</div> <img src="/public/Michael-Grieves.jpg" class="w-full h-56 object-cover rounded-lg shadow-xl border border-white/10" /> <p class="text-sm opacity-60 mt-3"> Fig. 2 · Michael Grieves at Marshall Space Flight Center  </p> </div>
<div v-click class="text-center transition-all duration-700 transform hover:scale-105"> <div class="text-amber-500 font-bold mb-2">2010</div> <img src="/public/John-Vickers.jpg" class="w-full h-56 object-cover rounded-lg shadow-xl border border-white/10" /> <p class="text-sm opacity-60 mt-3"> Fig. 3 · John Vickers during a visit to Marshall. Source: NASA/MSFC </p> </div>
</div>

---
layout: section
---

<!-- ============ 02 WHAT IS A DIGITAL TWIN ============ -->

<div class="text-7xl font-800 bg-gradient-to-r from-emerald-500 to-amber-500 bg-clip-text text-transparent leading-none">02</div>

# WHAT IS A DIGITAL TWIN?

---
layout: center
class: px-24
---

<div class="text-8xl text-emerald-500 leading-none opacity-70">“</div>

<div class="text-2xl italic leading-relaxed -mt-6">
A computational model of the system to be replicated, which in our case is all or part of a human patient, that is <b class="text-amber-500">bidirectionally connected</b> to the system, <b class="text-amber-500">periodically recalibrated</b> with patient data, and that provides <b class="text-amber-500">predictions</b> about the patient over time.
</div>

<div class="mt-10 text-right text-lg opacity-70">
  — <b>National Academies</b>
</div>

---

# A physical twin and its digital twin
<div class="flex items-center justify-center gap-6 mt-2">

  <div v-click="1" class="text-center">
    <div class="helix">
      <div v-for="i in 12" :key="i" class="row" :style="{ '--i': i }">
        <span class="rung"></span><span class="dot a"></span><span class="dot b"></span>
      </div>
    </div>
    <div class="font-bold mt-2">Patient</div>
    <div class="text-sm opacity-60">physical twin</div>
  </div>

  <div class="flex flex-col gap-6 text-5xl arrows">
    <span v-click="2" class="to-right">→</span>
    <span v-click="4" class="to-left">←</span>
  </div>

  <div v-click="3" class="text-center">
    <div class="helix digital">
      <div v-for="i in 12" :key="i" class="row" :style="{ '--i': i }">
        <span class="rung"></span><span class="dot a"></span><span class="dot b"></span>
      </div>
    </div>
    <div class="font-bold mt-2">Digital Twin</div>
    <div class="text-sm opacity-60">virtual replica</div>
  </div>

</div>

<div v-click.fade-in="5" class="text-center text-lg mt-4 opacity-90">
A virtual representation of a human or system, <b class="text-amber-500">constantly updated with real data</b>, to make better decisions.
</div>

<style>
.helix { position: relative; width: 120px; height: 230px; margin: 0 auto; }
.helix .row { position: absolute; left: 0; right: 0; top: calc(var(--i) * 18px); height: 12px; }
.helix .dot {
  position: absolute; left: 50%; top: 0; width: 12px; height: 12px; margin-left: -6px;
  border-radius: 50%; background: #10b981; box-shadow: 0 0 8px #10b981;
  animation: sway 3s ease-in-out infinite; animation-delay: calc(var(--i) * -0.25s);
}
.helix .dot.b { background: #f59e0b; box-shadow: 0 0 8px #f59e0b; animation-delay: calc(var(--i) * -0.25s - 1.5s); }
.helix.digital .dot.a { background: #22d3ee; box-shadow: 0 0 8px #22d3ee; }
.helix.digital .dot.b { background: #a78bfa; box-shadow: 0 0 8px #a78bfa; }
.helix .rung {
  position: absolute; left: 50%; top: 5px; width: 80px; height: 2px; margin-left: -40px;
  background: rgba(150,150,150,.5); animation: rung 3s linear infinite; animation-delay: calc(var(--i) * -0.25s);
}
@keyframes sway { 0%,100% { transform: translateX(-40px) scale(.7); } 50% { transform: translateX(40px) scale(1.2); } }
@keyframes rung { 0%,50%,100% { transform: scaleX(1); } 25%,75% { transform: scaleX(.05); } }
.arrows .to-right { animation: nudge-r 1.4s ease-in-out infinite; }
.arrows .to-left { animation: nudge-l 1.4s ease-in-out infinite; }
@keyframes nudge-r { 50% { transform: translateX(10px); } }
@keyframes nudge-l { 50% { transform: translateX(-10px); } }
</style>

---

# Simulation vs. Digital Twin

<div class="grid grid-cols-2 gap-8 mt-8">

  <div v-click.fade-in class="p-6 rounded-xl border border-gray-500/40 bg-gray-500/10">
    <div class="text-sm uppercase tracking-widest opacity-60">Simulation</div>
    <div class="text-3xl font-bold my-4">“How <span class="text-amber-500">should</span> it work?”</div>
    <ul class="text-lg opacity-80">
      <li>Predefined scenarios</li>
      <li>Static snapshots in time</li>
    </ul>
  </div>

  <div v-click.fade-in class="p-6 rounded-xl border border-emerald-500/60 bg-emerald-500/10">
    <div class="flex items-center justify-between">
      <div class="text-sm uppercase tracking-widest opacity-60">Digital Twin</div>
      <div class="live text-xs font-bold px-2 py-1 rounded bg-red-500 text-white">● LIVE</div>
    </div>
    <div class="text-3xl font-bold my-4">“How <span class="text-emerald-500">is</span> it working?”</div>
    <ul class="text-lg opacity-80">
      <li>Active representation</li>
      <li>Real-time data</li>
    </ul>
  </div>
</div>

<style>
.live { animation: blink 1.2s ease-in-out infinite; }
@keyframes blink { 50% { opacity: .35; } }
</style>

---
layout: section
---

<!-- ============ 03 CURRENT LANDSCAPE ============ -->

<div class="text-7xl font-800 bg-gradient-to-r from-emerald-500 to-amber-500 bg-clip-text text-transparent leading-none">03</div>

# CURRENT LANDSCAPE

---

# Old roots, young technology

<p class="opacity-70 -mt-2">
  Its origins go back decades, yet it is a relatively recent field.
</p>

<div class="mt-8 flex flex-col gap-5 text-lg">
  <!-- Construction -->
  <div v-click.fade="1">
    <div class="flex justify-between">
      <span> Construction</span>
      <span class="opacity-60 text-sm">
        simulate accidents · control processes in real time
      </span>
    </div>
    <div class="progress-track">
      <div class="progress-bar progress-92">
        <div class="shine"></div>
      </div>
    </div>
  </div>
  <!-- Aeronautics -->
  <div v-click.fade="1">
    <div class="flex justify-between">
      <span> Aeronautics</span>
      <span class="opacity-60 text-sm">
        predict failures without taking risks
      </span>
    </div>
    <div class="progress-track">
      <div class="progress-bar progress-83">
        <div class="shine"></div>
      </div>
    </div>
  </div>
  <!-- Automotive -->
  <div v-click.fade="1">
    <div class="flex justify-between">
      <span> Automotive</span>
      <span class="opacity-60 text-sm">
        industrial sector: where it is most developed
      </span>
    </div>
    <div class="progress-track">
      <div class="progress-bar progress-83">
        <div class="shine"></div>
      </div>
    </div>
  </div>
  <!-- Healthcare -->
  <div v-click.fade="2">
    <div class="flex justify-between">
      <span> Healthcare</span>
      <span class="text-amber-500 text-sm font-bold">
        still at an early stage
      </span>
    </div>
    <div class="progress-track">
      <div class="progress-bar healthcare">
        <div class="shine healthcare-shine"></div>
      </div>
    </div>
  </div>
</div>

<style>

/* Track */
.progress-track {
  height: 16px;
  margin-top: 6px;

  background: rgba(128,128,128,.16);

  border-radius: 999px;
  overflow: hidden;
}
/* Base bar */
.progress-bar {
  position: relative;
  height: 100%;
  border-radius: 999px;
  transform-origin: left;
  animation: grow-bar 1.2s cubic-bezier(.22,1,.36,1) both;
  overflow: hidden;
}
/* Green bars */
.progress-92 {
  width: 92%;
  background: #10b981;

  box-shadow:
    0 0 10px rgba(16,185,129,.35),
    0 0 25px rgba(16,185,129,.15);
}

.progress-83 {
  width: 83%;
  background: #10b981;

  box-shadow:
    0 0 10px rgba(16,185,129,.35),
    0 0 25px rgba(16,185,129,.15);
}


/* Healthcare */

.healthcare {
  width: 17%;
  background: #f59e0b;

  box-shadow:
    0 0 8px rgba(245,158,11,.25);
}


/* Moving green light */

.shine {
  position: absolute;
  top: 0;
  left: -40%;

  width: 40%;
  height: 100%;

  background: linear-gradient(
    90deg,
    transparent,
    rgba(255,255,255,.55),
    transparent
  );

  animation: shine-move 2.4s ease-in-out infinite;
}


/* Healthcare has a much more subtle shine */

.healthcare-shine {
  animation-duration: 4s;
  opacity: .25;
}


/* Bar entrance */

@keyframes grow-bar {
  from {
    transform: scaleX(0);
  }

  to {
    transform: scaleX(1);
  }
}


/* Moving highlight */

@keyframes shine-move {
  0% {
    left: -40%;
  }

  60% {
    left: 110%;
  }

  100% {
    left: 110%;
  }
}

</style>

---

# Barça Innovation Hub

<div class="relative mt-8 pl-10">
  <div class="absolute left-3 top-2 bottom-2 w-0.5 bg-gray-500/40"></div>
  <div class="relative mb-8">
    <div class="absolute -left-10 top-1 w-6 h-6 rounded-full bg-emerald-500"></div>
    <div v-click.fade class="text-3xl font-800 text-emerald-500">2021 · IoTwins</div>
    <ul v-click.fade-in class="text-lg mt-2 opacity-90">
      <li>Pilot work with the <b>Barcelona Supercomputing Center</b></li>
      <li>A digital twin of the stadium to simulate scenarios</li>
      <li>Goal: anticipate fan behaviour on match days</li>
    </ul>
  </div>
  <div class="relative">
    <div class="absolute -left-10 top-1 w-6 h-6 rounded-full bg-amber-500"></div>
    <div v-click.fade class="text-3xl font-800 text-amber-500">2025 · Digital Twins</div>
    <ul v-click.fade-in class="text-lg mt-2 opacity-90">
      <li>Work with the <b>Made of Genes</b></li>
      <li>A smaller-scale digital twin of <b>each football player</b></li>
      <li>Built from molecular data (<i>sportnomics</i>) and AI</li>
      <li>Goals: prevent injuries, maximise performance, extend athletic longevity</li>
    </ul>
  </div>
</div>
---
layout: section
---

<!-- ============ 04 DIGITAL TWINS IN HEALTHCARE ============ -->

<div class="text-7xl font-800 bg-gradient-to-r from-emerald-500 to-amber-500 bg-clip-text text-transparent leading-none">04</div>

# DIGITAL TWINS IN HEALTHCARE

---

# Artificial Pancreas
 
<p class="opacity-70 -mt-2">One of the first digital twin-like systems: the artificial pancreas. Two essential parts:</p>
<div class="flex items-center justify-center gap-4 mt-10 text-center">
  <div v-click class="p-5 rounded-xl bg-emerald-500/20 border border-emerald-500/50 w-64"><div class="text-xs opacity-60">PART 1</div><div class="text-4xl">🩸</div><b>Measures glucose</b><div class="text-sm opacity-70">continuously</div></div>
  <div v-click class="text-3xl">→</div>
  <div v-click class="p-5 rounded-xl bg-amber-500/20 border border-amber-500/50 w-64"><div class="text-xs opacity-60">PART 2</div><div class="text-4xl">💉</div><b>Infuses insulin</b><div class="text-sm opacity-70">syringe device, only when needed</div></div>
</div>

---

# Smart Continuous Glucose Monitoring
<div class="cgm">
  <div
    style="grid-area:1/2/2/4;align-self:end"
    class="text-green-500 font-bold text-left"
  >
    Algorithmically smart CGM sensor
  </div>
  <div style="grid-area:1/4" class="inp">
    BG references<br>(e.g. SMBG) ↓
  </div>
  <div style="grid-area:1/5" class="inp dashed">
    Other information, e.g. Meal, insulin, exercise<br>
    (if available) ↓
  </div>
  <div class="gbg" style="grid-area:2/2/3/6"></div>
  <div
    class="st nx"
    style="grid-area:2/1;background:#3b82f6;color:#fff"
  >
    Patient
  </div>
  <div
    class="st nx"
    style="grid-area:2/2;background:#111;color:#fff"
  >
    CGM sensor
  </div>
  <div class="st nx" style="grid-area:2/3">
    Denoising module
  </div>
  <div class="st nx" style="grid-area:2/4">
    Enhancement module
  </div>
  <div class="st" style="grid-area:2/5">
    Prediction module
  </div>
  <div v-click style="grid-area:3/2">
    <b>↓ Original CGM data</b><br>
    <span class="text-red-500">
      ✗ measurement noise<br>
      ✗ systematic under/over-estimation<br>
      ✗ delayed alerts generation
    </span>
  </div>
  <div v-click style="grid-area:3/3">
    <b>↓ Denoised CGM data</b><br>
    <span class="text-green-500">
      ✓ reduction of measurement noise
    </span>
  </div>
  <div v-click style="grid-area:3/4">
    <b>↓ Enhanced CGM data</b><br>
    <span class="text-green-500">
      ✓ fewer systematic under/over-estimations
    </span>
  </div>
  <div v-click style="grid-area:3/5">
    <b>↓ Predicted CGM data</b><br>
    <span class="text-green-500">
      ✓ preventive alarms to compensate for delays
    </span>
  </div>
</div>
<!-- WHAT'S NEW -->
<div
  v-click
  class="whats-new"
>
  <div class="whats-icon">✦</div>
  <div>
    <div class="whats-title">
      What's new
    </div>
    <div class="whats-text">
      The artificial pancreas evolves from a
      <b>reactive</b> measuring system to a
      <b>predictive and personalised physiological model</b>
      that simulates the glucose–insulin network.
    </div>
  </div>
</div>

<style>

.cgm {
  display: grid;
  grid-template-columns: repeat(5, 1fr);

  column-gap: 24px;
  row-gap: 4px;

  font-size: 10.5px;
  text-align: center;

  margin-top: -50px;
}

.gbg {
  background: #22c55e20;
  border: 2px solid #22c55e;
  border-radius: 12px;

  margin: -6px -10px;
}

.st {
  position: relative;
  z-index: 1;

  background: #fff;
  color: #111;

  border-radius: 6px;

  padding: 9px 4px;

  font-weight: 600;

  align-self: center;
}

.nx::after {
  content: '→';

  position: absolute;
  right: -19px;
  top: 50%;

  transform: translateY(-50%);

  color: #888;
  font-size: 15px;
}

.inp {
  padding: 3px;
  opacity: .8;
}

.dashed {
  border: 1px dashed #888;
  border-radius: 6px;
}


/* =========================
   WHAT'S NEW
   ========================= */

.whats-new {
  margin-top: 12px;

  display: flex;
  align-items: center;
  gap: 12px;

  padding: 10px 16px;

  border-radius: 10px;

  background: rgba(16, 185, 129, .08);

  border: 1px solid rgba(16, 185, 129, .45);

  box-shadow:
    0 0 18px rgba(16, 185, 129, .08);

  font-size: 13px;

  animation: whats-in .6s ease-out both;
}


.whats-icon {
  flex-shrink: 0;

  width: 32px;
  height: 32px;

  display: flex;
  align-items: center;
  justify-content: center;

  border-radius: 50%;

  background: #10b981;
  color: white;

  font-size: 17px;

  box-shadow:
    0 0 12px rgba(16, 185, 129, .45);

  animation: pulse-green 2s ease-in-out infinite;
}


.whats-title {
  color: #10b981;

  font-weight: 700;

  font-size: 14px;

  margin-bottom: 2px;
}


.whats-text {
  opacity: .85;

  line-height: 1.35;
}


@keyframes whats-in {

  from {
    opacity: 0;
    transform: translateY(8px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }

}


@keyframes pulse-green {

  0%, 100% {
    box-shadow:
      0 0 8px rgba(16, 185, 129, .25);
  }

  50% {
    box-shadow:
      0 0 18px rgba(16, 185, 129, .65);
  }

}

</style>

---

 
# Cardiac Digital Twins
 
<div class="grid grid-cols-2 gap-10 items-center mt-4">
  <div class="text-center">
    <div class="beat text-9xl">❤️</div>
    <svg viewBox="0 0 240 60" class="w-full"><path class="ecg" d="M0 30 H40 l6 -8 l6 8 H80 l5 8 l7 -38 l7 46 l5 -16 H140 q12 -18 26 0 H240" fill="none" stroke="#ef4444" stroke-width="2.5"/></svg>
  </div>
  <div class="text-lg">
    <p>Digital twins built on <b>models of cardiac electrophysiology</b>.</p>
    <p class="text-amber-500 font-bold">Goal: test and optimise personalised monitoring and treatment strategies, safely and in real time.</p>
    <div v-click class="mt-4 p-3 rounded-lg bg-emerald-500/15 border border-emerald-500/40">① <b>Anatomical twinning</b><br><span class="text-sm opacity-70">a 3D copy of the patient's heart</span></div>
    <div v-click class="mt-3 p-3 rounded-lg bg-amber-500/15 border border-amber-500/40">② <b>Functional twinning</b><br><span class="text-sm opacity-70">simulating how it works electrically</span></div>
  </div>
</div>
<style>
.beat { display: inline-block; animation: beat 1.2s ease-in-out infinite; }
@keyframes beat { 0%,100% { transform: scale(1); } 15% { transform: scale(1.22); } 30% { transform: scale(1); } 45% { transform: scale(1.12); } }
.ecg { stroke-dasharray: 420; stroke-dashoffset: 420; animation: draw 2.4s linear infinite; }
@keyframes draw { to { stroke-dashoffset: 0; } }
</style>
 
---

# ① Anatomical Twinning

<div class="grid grid-cols-2 gap-8 mt-6 text-center items-stretch">
  <div v-click.fade-in class="p-4 rounded-xl bg-blue-500/15 border border-blue-500/40 flex flex-col justify-between
           transition-all duration-700 ease-out
           hover:scale-[1.03] hover:shadow-lg hover:shadow-blue-500/10"
  >
    <div>
      <div class="overflow-hidden rounded mb-3">
        <img
          src="/public/segmentation.png"
          class="h-40 mx-auto object-contain transition-transform duration-700 hover:scale-105"
        />
      </div>
      <b class="block mt-1 text-blue-400
                animate-[fadeIn_0.8s_ease-out]">
        Segmentation
      </b>
      <p class="text-s opacity-80 mt-2">
        Like colouring-in a scan: a CNN traces outlines and separates tissue
        from cavities. Then it is corrected manually.
      </p>
    </div>
  </div>
  <div
    v-click.fade-in
    class="p-4 rounded-xl bg-emerald-500/15 border border-emerald-500/40
           flex flex-col justify-between
           transition-all duration-700 ease-out
           hover:scale-[1.03] hover:shadow-lg hover:shadow-emerald-500/10
           animate-[slideIn_0.8s_ease-out]"
  >
    <div>
      <div class="overflow-hidden rounded mb-3">
        <img
          src="/public/meshing.png"
          class="h-40 mx-auto object-contain transition-transform duration-700 hover:scale-105"
        />
      </div>
      <b class="block mt-1 text-emerald-400">
        Meshing
      </b>
      <p class="text-s opacity-80 mt-2">
        Like the wireframe of a 3D character: the outlines become a 3D mesh,
        using <b>UVC</b>, the "GPS" of the heart's regions.
      </p>
    </div>
  </div>
</div>
<div
  v-click.fade-in
  class="mt-3 text-center text-lg
         animate-[fadeInUp_0.8s_ease-out]"
>
  <span class="inline-block animate-pulse">➜</span>
  <b class="text-emerald-500">Result:</b>
  a patient-specific 3D model of the heart
</div>
<div
  class="absolute bottom-1 right-6 text-xs opacity-50
         transition-opacity duration-500 hover:opacity-100"
>
  Figure adapted from the source paper
</div>


<style>
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateX(30px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(15px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>

---

# ② Functional Twinning
 
<div class="grid grid-cols-3 gap-6 mt-4 text-center">
  <div v-click.fade-in class="p-4 rounded-xl bg-blue-500/15 border border-blue-500/40">
    <div class="text-4xl"></div><b class="block mt-1">Reference frame</b>
    <p class="text-sm opacity-70">A standard coordinate system laid over each patient's anatomy, like fitting the same map grid to every heart.</p>
  </div>
  <div v-click.fade-in class="p-4 rounded-xl bg-purple-500/15 border border-purple-500/40">
    <div class="text-4xl"></div><b class="block mt-1">Feature vector</b>
    <p class="text-sm opacity-70">The heart's "ID card": its geometry and anatomy as numbers the model can process.</p>
  </div>
  <div v-click.fade-in class="p-4 rounded-xl bg-amber-500/15 border border-amber-500/40">
    <div class="text-4xl"></div><b class="block mt-1">Forward ECG model</b>
    <p class="text-sm opacity-70">Maths that predicts the ECG the patient <i>should</i> show: y<sub>s</sub>(t) = f(ω, t)</p>
  </div>
</div>
<div v-click.fade-in class="mt-6 p-4 rounded-xl border border-dashed border-gray-500/60 text-center">
  <div class="flex items-center justify-center gap-4 text-sm">
    <div>Real 12-lead ECG<br>y<sub>m</sub>(t)
      <svg viewBox="0 0 120 40" class="w-32"><path class="ecg2" d="M0 20 H20 l4 -5 l4 5 H45 l3 5 l4 -25 l4 30 l3 -10 H85 q8 -12 17 0 H120" fill="none" stroke="#22c55e" stroke-width="2"/></svg></div>
    <div class="text-2xl">⇄</div>
    <div>Simulated ECG<br>y<sub>s</sub>(t)
      <svg viewBox="0 0 120 40" class="w-32"><path class="ecg2" d="M0 20 H20 l4 -5 l4 5 H45 l3 5 l4 -25 l4 30 l3 -10 H85 q8 -12 17 0 H120" fill="none" stroke="#ef4444" stroke-width="2"/></svg></div>
    <div class="text-2xl">→</div>
    <div class="text-left">Compare the error <b>L</b>(y<sub>m</sub>, y<sub>s</sub>)<br><span class="tune"> adjust parameters and repeat</span><br></div>
  </div>
</div>
<style>
.ecg2 { stroke-dasharray: 260; stroke-dashoffset: 260; animation: draw2 2s linear infinite; }
@keyframes draw2 { to { stroke-dashoffset: 0; } }
.tune { display: inline-block; animation: wob 1s ease-in-out infinite; }
@keyframes wob { 50% { transform: rotate(-12deg); } }
</style>

---
layout: section
---

<!-- ============ 05 CLINICAL CASE ============ -->

<div class="text-7xl font-800 bg-gradient-to-r from-emerald-500 to-amber-500 bg-clip-text text-transparent leading-none">05</div>

# CLINICAL CASE

---

# A bodybuilder's sudden collapse
 
<div class="grid grid-cols-2 gap-8 mt-4 text-center">
  <div class="p-4 rounded-xl bg-emerald-500/15 border border-emerald-500/50">
    <div class="text-xs uppercase tracking-widest opacity-60">What we see</div>
    <div class="text-6xl my-1">💪</div><b>Peak physical condition</b>
  </div>
  <div v-click class="p-4 rounded-xl bg-red-500/15 border border-red-500/60 alarm">
    <div class="text-xs uppercase tracking-widest opacity-60">What was hidden</div>
    <div class="text-6xl my-1">❤️‍🔥</div><b>An undetected cardiac condition</b>
  </div>
</div>
<div class="grid grid-cols-3 gap-4 mt-5 text-center text-sm">
  <div v-click class="p-3 rounded-lg bg-gray-500/15"> <b>Looking fit ≠ a healthy heart</b></div>
  <div v-click class="p-3 rounded-lg bg-gray-500/15"> <b>Extreme exercise on a diseased heart can be lethal</b></div>
  <div v-click class="p-3 rounded-lg bg-gray-500/15"> <b>Simple, cheap prevention: an ECG</b></div>
</div>
<div v-click class="mt-5 p-3 rounded-lg bg-amber-500 text-black text-center font-bold">
Cardiac Digital Twins could predict fatal arrhythmias <i>in silico</i>, before they happen in real life.
</div>
<style>
.alarm { animation: glow 1.4s ease-in-out infinite; }
@keyframes glow { 50% { box-shadow: 0 0 22px #ef4444aa; } }
</style>

---
layout: section
---

<!-- ============ 06 CHALLENGES ============ -->

<div class="text-7xl font-800 bg-gradient-to-r from-emerald-500 to-amber-500 bg-clip-text text-transparent leading-none">06</div>

# CHALLENGES

---

# Four walls to climb
 
<div class="grid grid-cols-2 gap-5 mt-4 text-sm">
  <div v-click class="p-4 mt-1 rounded-xl bg-blue-500/15 border-l-4 border-blue-500">
 <div class="text-3xl"> <b class="mt-1 text-lg align-middle">Biological knowledge</b></div>
    <p class="opacity-80">We still have incomplete knowledge of human biology.</p>
  </div>
  <div v-click class="p-4 rounded-xl bg-emerald-500/15 border-l-4 border-emerald-500">
    <div class="text-3xl"> <b class="text-lg align-middle">Data</b></div>
    <p class="opacity-80">Enough quantity <i>and</i> quality: heterogeneous sources, and continuous non-invasive collection is still in development or too noisy.</p>
  </div>
  <div v-click class="p-4 rounded-xl bg-amber-500/15 border-l-4 border-amber-500">
    <div class="text-3xl"> <b class="text-lg align-middle">Computing</b></div>
    <p class="opacity-80">Heavy image-processing load, a segmentation bottleneck and a lack of automation.</p>
  </div>
  <div v-click class="p-4 rounded-xl bg-red-500/15 border-l-4 border-red-500">
    <div class="text-3xl"> <b class="text-lg align-middle">Privacy & security</b></div>
    <p class="opacity-80">Regulation is needed. Who controls the twin? Who owns it? What can be done with it?</p>
  </div>
</div>

---
layout: section
---

<!-- ============ 07 CONCLUSION ============ -->

<div class="text-7xl font-800 bg-gradient-to-r from-emerald-500 to-amber-500 bg-clip-text text-transparent leading-none">07</div>

# CONCLUSION

---
layout: center
class: text-center
---
 
# A turning point in modern medicine
 
<div class="mt-10 flex flex-col gap-8 text-4xl font-bold">
  <div class="flex items-center justify-center gap-6">
    <span class="opacity-70">Curative</span>
    <span class="opacity-50">→</span>
    <span v-click class="text-emerald-500">Preventive</span>
  </div>
  <div class="flex items-center justify-center gap-6">
    <span class="opacity-70">Generalised</span>
    <span class="opacity-50">→</span>
    <span v-click class="text-amber-500">Personalised</span>
  </div>
</div>
<div v-click class="mt-10 text-xl opacity-80">A big step: medicine that anticipates instead of reacting.</div>
