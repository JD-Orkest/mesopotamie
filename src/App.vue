<script setup>
/**
 * App.vue — Composant racine
 * Gère : navigation sticky, barre de progression dorée, ScrollTrigger global.
 */
import { onMounted, onUnmounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

import TheNavigation       from './components/TheNavigation.vue'
import HeroSection         from './components/HeroSection.vue'
import EpoquesSection      from './components/EpoquesSection.vue'
import ChaoskampfSection   from './components/ChaoskampfSection.vue'
import TransmissionSection from './components/TransmissionSection.vue'
import RituelsSection      from './components/RituelsSection.vue'
import TheFooter           from './components/TheFooter.vue'

gsap.registerPlugin(ScrollTrigger)

const navVisible = ref(true)
let lastScrollY = 0

function handleScroll() {
  const currentY = window.scrollY

  // Navigation : masquée au scroll vers le bas, visible au scroll vers le haut
  navVisible.value = currentY < lastScrollY || currentY < 80
  lastScrollY = currentY

  // Barre de progression dorée
  const docH = document.documentElement.scrollHeight - window.innerHeight
  const progress = docH > 0 ? (currentY / docH) * 100 : 0
  const bar = document.getElementById('progress-bar')
  if (bar) bar.style.width = `${progress}%`
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll, { passive: true })

  // Animation globale : révéler tous les éléments .reveal au scroll
  gsap.utils.toArray('.reveal').forEach((el) => {
    gsap.to(el, {
      opacity: 1,
      y: 0,
      duration: 1,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: el,
        start: 'top 88%',
        once: true,
      },
    })
  })
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
  ScrollTrigger.getAll().forEach(t => t.kill())
})
</script>

<template>
  <div id="site-wrapper">
    <TheNavigation :visible="navVisible" />

    <main>
      <HeroSection />
      <EpoquesSection />
      <ChaoskampfSection />
      <TransmissionSection />
      <RituelsSection />
    </main>

    <TheFooter />
  </div>
</template>

<style>
#site-wrapper {
  position: relative;
}
</style>
