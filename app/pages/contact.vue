<script setup lang="ts">

useSeoMeta({ title: 'contato' })

const contacts = [
  {
    label: 'LinkedIn',
    handle: '/in/marcos-afonso',
    href: 'https://linkedin.com/in/marcos-afonso',
    icon: 'lucide:linkedin',
  },
  {
    label: 'Email',
    handle: 'marcos.afonsoo@outlook.com',
    href: 'mailto:marcos.afonsoo@outlook.com',
    icon: 'lucide:mail',
  },
  {
    label: 'GitHub',
    handle: '@marcosafns',
    href: 'https://github.com/marcosafns',
    icon: 'lucide:github',
  },
  {
    label: 'Instagram',
    handle: '@marcos.afonsooo',
    href: 'https://instagram.com/marcos.afonsooo',
    icon: 'lucide:instagram',
  },
]
</script>

<template>
  <div class="min-h-screen bg-[#07070a] flex flex-col items-center justify-center relative overflow-hidden px-6">

    <!-- Orb -->
    <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[500px] h-[500px] bg-purple-500/6 rounded-full blur-[120px] pointer-events-none" />

    <!-- Voltar -->
    <div class="absolute top-8 left-10 back-link">
      <NuxtLink
        to="/"
        class="group flex items-center gap-2 font-mono text-[11px] tracking-[0.2em] uppercase text-[#5c5470] hover:text-purple-400 transition-colors duration-300"
      >
        <Icon name="lucide:arrow-left" class="w-3 h-3 group-hover:-translate-x-1 transition-transform duration-300" />
        Voltar
      </NuxtLink>
    </div>

    <div class="relative z-10 flex flex-col items-center gap-12 w-full max-w-md">

      <!-- Título -->
      <div class="flex flex-col items-center gap-3 text-center">
        <div class="title-eyebrow flex items-center gap-3">
          <span class="w-6 h-px bg-purple-500/50" />
          <p class="font-mono text-[10px] tracking-[0.3em] uppercase text-[#5c5470]">Fale comigo</p>
          <span class="w-6 h-px bg-purple-500/50" />
        </div>
        <h1
          class="title-reveal font-outfit font-extrabold leading-none tracking-tight text-[#f1eeff]"
          style="font-size: clamp(40px, 8vw, 80px)"
        >
          contato
        </h1>
      </div>

      <!-- Cards -->
      <div class="cards-reveal grid grid-cols-2 gap-3 w-full">
        <NuxtLink
          v-for="(item, i) in contacts"
          :key="item.label"
          :to="item.href"
          :target="item.href.startsWith('http') ? '_blank' : undefined"
          :rel="item.href.startsWith('http') ? 'noopener noreferrer' : undefined"
          external
          class="group flex flex-col items-start gap-5 p-6 bg-[#0d0d12] border border-white/5 hover:border-purple-500/25 hover:bg-purple-500/[0.04] transition-all duration-300 hover:-translate-y-1 hover:shadow-[0_12px_40px_rgba(168,85,247,0.1)]"
          :style="{ animationDelay: `${0.5 + i * 0.08}s` }"
        >
          <div class="w-9 h-9 rounded-xl bg-white/5 border border-white/5 flex items-center justify-center group-hover:bg-purple-500/15 group-hover:border-purple-500/20 transition-all duration-300">
            <Icon :name="item.icon" class="w-4 h-4 text-[#5c5470] group-hover:text-purple-400 transition-colors duration-300" />
          </div>
          <div class="flex flex-col gap-0.5">
            <span class="font-outfit font-semibold text-sm text-[#f1eeff] group-hover:text-purple-200 transition-colors duration-300">
              {{ item.label }}
            </span>
            <span class="font-mono text-[10px] text-[#5c5470] tracking-wide">{{ item.handle }}</span>
          </div>
          <Icon name="lucide:arrow-up-right" class="w-3 h-3 text-[#5c5470]/30 group-hover:text-purple-400 ml-auto self-end transition-all duration-300 group-hover:translate-x-0.5 group-hover:-translate-y-0.5" />
        </NuxtLink>
      </div>

    </div>
  </div>
</template>

<style scoped>
.back-link     { animation: fadeIn   0.6s ease                        0.1s both; }
.title-eyebrow { animation: fadeDown 0.7s cubic-bezier(0.16,1,0.3,1) 0.2s both; }
.title-reveal  { animation: slideUp  0.9s cubic-bezier(0.16,1,0.3,1) 0.3s both; }
.cards-reveal  { animation: fadeUp   0.8s cubic-bezier(0.16,1,0.3,1) 0.5s both; }

@keyframes slideUp  { from { opacity:0; transform:translateY(40px); } to { opacity:1; transform:translateY(0); } }
@keyframes fadeUp   { from { opacity:0; transform:translateY(16px); } to { opacity:1; transform:translateY(0); } }
@keyframes fadeDown { from { opacity:0; transform:translateY(-12px);} to { opacity:1; transform:translateY(0); } }
@keyframes fadeIn   { from { opacity:0; } to { opacity:1; } }
</style>