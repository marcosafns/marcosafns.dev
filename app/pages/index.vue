<script setup lang="ts">

useSeoMeta({ title: 'marcosafns dev' })

interface Particle {
  x: number; y: number
  vx: number; vy: number
  life: number; maxLife: number
  size: number
}

const canvasRef = ref<HTMLCanvasElement | null>(null)

onMounted(() => {
  const canvas = canvasRef.value!
  const ctx = canvas.getContext('2d')!

  canvas.width = window.innerWidth
  canvas.height = window.innerHeight

  window.addEventListener('resize', () => {
    canvas.width = window.innerWidth
    canvas.height = window.innerHeight
  })

  const particles: Particle[] = []

  let mouseX = window.innerWidth / 2
  let mouseY = window.innerHeight / 2
  let lastX = mouseX
  let lastY = mouseY

  window.addEventListener('mousemove', (e) => {
    mouseX = e.clientX
    mouseY = e.clientY
  })

  window.addEventListener('click', (e) => {
    for (let i = 0; i < 40; i++) {
      const angle = (i / 40) * Math.PI * 2
      const speed = 1.5 + Math.random() * 4
      particles.push({
        x: e.clientX,
        y: e.clientY,
        vx: Math.cos(angle) * speed,
        vy: Math.sin(angle) * speed - 1,
        life: 1,
        maxLife: 80 + Math.random() * 60,
        size: 1.5 + Math.random() * 2.5,
      })
    }
  })

  function spawnTrail() {
    const dx = mouseX - lastX
    const dy = mouseY - lastY
    const dist = Math.sqrt(dx * dx + dy * dy)

    if (dist > 2) {
      const count = Math.min(Math.floor(dist / 4), 6)
      for (let i = 0; i < count; i++) {
        const t = i / count
        particles.push({
          x: lastX + dx * t + (Math.random() - 0.5) * 6,
          y: lastY + dy * t + (Math.random() - 0.5) * 6,
          vx: (Math.random() - 0.5) * 0.6,
          vy: (Math.random() - 0.5) * 0.6 - 0.3,
          life: 1,
          maxLife: 60 + Math.random() * 60,
          size: 1 + Math.random() * 2,
        })
      }
      lastX = mouseX
      lastY = mouseY
    }
  }

  function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height)
    spawnTrail()

    for (let i = particles.length - 1; i >= 0; i--) {
      const p = particles[i]
      if (!p) continue

      p.x += p.vx
      p.y += p.vy
      p.vy += 0.01
      p.life -= 1 / p.maxLife

      if (p.life <= 0) {
        particles.splice(i, 1)
        continue
      }

      const alpha = p.life * 0.6
      const radius = p.size * p.life

      const gradient = ctx.createRadialGradient(p.x, p.y, 0, p.x, p.y, radius * 6)
      gradient.addColorStop(0, `rgba(192, 132, 252, ${alpha})`)
      gradient.addColorStop(1, `rgba(139, 92, 246, 0)`)

      ctx.beginPath()
      ctx.arc(p.x, p.y, radius * 6, 0, Math.PI * 2)
      ctx.fillStyle = gradient
      ctx.fill()

      ctx.beginPath()
      ctx.arc(p.x, p.y, radius, 0, Math.PI * 2)
      ctx.fillStyle = `rgba(232, 220, 255, ${alpha * 0.9})`
      ctx.fill()
    }

    requestAnimationFrame(draw)
  }

  draw()
})

const x = ref(0)
const y = ref(0)

function onMouseMove(e: MouseEvent) {
  x.value = (e.clientX / window.innerWidth - 0.5) * 40
  y.value = (e.clientY / window.innerHeight - 0.5) * 40
}
</script>

<template>
  <div
    class="min-h-screen bg-[#07070a] flex flex-col items-center justify-center relative overflow-hidden"
    @mousemove="onMouseMove"
  >

    <!-- Canvas rastro -->
    <canvas ref="canvasRef" class="absolute inset-0 pointer-events-none z-0" />

    <!-- Orbs -->
    <div
      class="absolute w-[600px] h-[600px] bg-purple-500/8 rounded-full blur-[130px] pointer-events-none transition-transform duration-700 ease-out"
      :style="{ transform: `translate(calc(-50% + ${x}px), calc(-50% + ${y}px))`, top: '50%', left: '50%' }"
    />
    <div
      class="absolute w-[300px] h-[300px] bg-violet-600/8 rounded-full blur-[90px] pointer-events-none transition-transform duration-1000 ease-out"
      :style="{ transform: `translate(calc(-50% + ${-x * 0.5}px), calc(-50% + ${-y * 0.5}px))`, top: '45%', left: '55%' }"
    />

    <!-- Contato -->
    <div class="absolute top-8 right-10 contact-link">
      <NuxtLink
        to="/contact"
        class="group flex items-center gap-2 font-mono text-[11px] tracking-[0.2em] uppercase text-[#5c5470] hover:text-purple-400 transition-colors duration-300"
      >
        Contato
        <Icon name="lucide:arrow-up-right" class="w-3 h-3 group-hover:translate-x-0.5 group-hover:-translate-y-0.5 transition-transform duration-300" />
      </NuxtLink>
    </div>

    <!-- Conteúdo -->
    <div class="relative z-10 flex flex-col items-center gap-6 text-center">

      <div class="eyebrow flex items-center gap-3">
        <span class="w-6 h-px bg-purple-500/50" />
        <p class="font-mono text-[10px] tracking-[0.3em] uppercase text-[#5c5470]">Full Stack Developer</p>
        <span class="w-6 h-px bg-purple-500/50" />
      </div>

      <div class="overflow-hidden">
        <h1
          class="name-reveal font-outfit font-extrabold leading-none tracking-tight text-[#f1eeff]"
          style="font-size: clamp(72px, 13vw, 160px)"
        >
          afns
        </h1>
      </div>

      <div class="overflow-hidden -mt-4">
        <h2
          class="lastname-reveal font-outfit font-extrabold leading-none tracking-tight"
          style="font-size: clamp(24px, 5vw, 64px); -webkit-text-stroke: 1px rgba(168,85,247,0.4); color: transparent"
        >
          marcos
        </h2>
      </div>

      <div class="line-reveal w-32 h-px bg-gradient-to-r from-transparent via-purple-500/60 to-transparent" />

      <p class="desc-reveal font-mono text-[11px] tracking-[0.2em] uppercase text-[#5c5470] leading-relaxed">
        Construindo interfaces que<br>performam e impressionam
      </p>

    </div>
  </div>
</template>

<style scoped>
.eyebrow         { animation: fadeDown   0.7s cubic-bezier(0.16,1,0.3,1) 0.2s  both; }
.name-reveal     { animation: slideUp    1s   cubic-bezier(0.16,1,0.3,1) 0.4s  both; }
.lastname-reveal { animation: slideUp    1s   cubic-bezier(0.16,1,0.3,1) 0.55s both; }
.line-reveal     { animation: expandLine 0.8s cubic-bezier(0.16,1,0.3,1) 0.9s  both; }
.desc-reveal     { animation: fadeUp     0.7s cubic-bezier(0.16,1,0.3,1) 1.1s  both; }
.contact-link    { animation: fadeIn     0.6s ease                        1.3s  both; }

@keyframes slideUp    { from { opacity:0; transform:translateY(60px); } to { opacity:1; transform:translateY(0); } }
@keyframes fadeUp     { from { opacity:0; transform:translateY(16px); } to { opacity:1; transform:translateY(0); } }
@keyframes fadeDown   { from { opacity:0; transform:translateY(-16px);} to { opacity:1; transform:translateY(0); } }
@keyframes fadeIn     { from { opacity:0; } to { opacity:1; } }
@keyframes expandLine { from { opacity:0; transform:scaleX(0); } to { opacity:1; transform:scaleX(1); } }
</style>