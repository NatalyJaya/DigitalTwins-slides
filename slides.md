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

<div class="grid grid-cols-2 gap-10 mt-6">
  <div v-click class="text-center transition-all duration-700 transform hover:scale-105">
    <div class="text-amber-500 font-bold mb-2">1970</div>
    <img src="/Apolo13-Astronauts.jpg" class="w-full h-56 object-cover rounded-lg shadow-xl border border-white/10" />
    <p class="text-sm opacity-60 mt-3">Fig. 1 · Apollo 13 crew. Source: El Litoral</p>
  </div>
  
  <div v-click class="text-center transition-all duration-700 transform hover:scale-105">
    <div class="text-amber-500 font-bold mb-2">2002</div>
    <img src="/Michael-Grieves.jpg" class="w-full h-56 object-cover rounded-lg shadow-xl border border-white/10" />
    <p class="text-sm opacity-60 mt-3">Fig. 2 · Good Twin Better Twin - Michael Grieves at Marshall Space Flight Center</p>
  </div>
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

<!--
Next: 04 DIGITAL TWINS IN HEALTHCARE, 05 CLINICAL CASE, 06 CHALLENGES, 07 CONCLUSION
-->
