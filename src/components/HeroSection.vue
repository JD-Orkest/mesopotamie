<script setup>
/**
 * HeroSection.vue
 * Section Hero : titre massif "MÉSOPOTAMIE", sous-titre éditorial, scroll indicator.
 * GSAP : animation d'entrée staggerée au montage.
 */
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'

const heroRef   = ref(null)
const titleRef  = ref(null)
const subRef    = ref(null)
const introRef  = ref(null)
const scrollRef = ref(null)

onMounted(() => {
  const tl = gsap.timeline({ defaults: { ease: 'power4.out' } })

  tl.fromTo(titleRef.value,
    { y: 60, opacity: 0, clipPath: 'inset(0 0 100% 0)' },
    { y: 0,  opacity: 1, clipPath: 'inset(0 0 0% 0)',   duration: 1.4 }
  )
  .fromTo(subRef.value,
    { y: 30, opacity: 0 },
    { y: 0,  opacity: 1, duration: 1 },
    '-=0.8'
  )
  .fromTo(introRef.value,
    { y: 20, opacity: 0 },
    { y: 0,  opacity: 1, duration: 0.9 },
    '-=0.7'
  )
  .fromTo(scrollRef.value,
    { opacity: 0, y: 10 },
    { opacity: 1, y: 0,  duration: 0.8 },
    '-=0.4'
  )

  // Animation pulsée du scroll indicator
  gsap.to(scrollRef.value, {
    y: 12,
    repeat: -1,
    yoyo: true,
    duration: 1.2,
    ease: 'sine.inOut',
    delay: 2.5,
  })
})
</script>

<template>
  <section id="hero" ref="heroRef" class="hero-section">
    <!-- Grille de fond décorative -->
    <div class="hero-bg-grid" aria-hidden="true">
      <div v-for="n in 6" :key="n" class="grid-line"></div>
    </div>

    <div class="container hero-content">
      <!-- Sur-titre -->
      <p ref="subRef" class="label-caps hero-subtitle">
        Archive numérique — Mythologie comparée
      </p>

      <!-- Titre principal display-xl -->
      <h1 ref="titleRef" class="hero-title" lang="fr">
        MÉSOPOTAMIE
      </h1>

      <!-- Texte d'introduction -->
      <p ref="introRef" class="hero-intro">
        Une curation numérique retraçant la lignée du mythe.<br />
        Du combat cosmique de Babylone au folklore contemporain de l'Europe.
      </p>
    </div>

    <!-- Scroll indicator -->
    <div ref="scrollRef" class="scroll-indicator" aria-hidden="true">
      <span class="scroll-line"></span>
    </div>
  </section>
</template>

<style scoped>
.hero-section {
  position: relative;
  min-height: 100svh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  overflow: hidden;
}

/* Grille décorative en arrière-plan */
.hero-bg-grid {
  position: absolute;
  inset: 0;
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  pointer-events: none;
  z-index: 0;
}

.grid-line {
  border-right: 1px solid rgba(230, 223, 211, 0.04);
}

/* Contenu */
.hero-content {
  position: relative;
  z-index: 1;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 28px;
  padding-top: 120px;
  padding-bottom: 80px;
}

.hero-subtitle {
  opacity: 0; /* état initial pour GSAP */
  color: var(--color-gold);
  max-width: none;
}

/* Titre immense — s'étend sur toute la largeur */
.hero-title {
  opacity: 0; /* état initial pour GSAP */
  font-size: var(--text-display-xl);
  font-weight: 700;
  letter-spacing: -0.03em;
  line-height: 0.95;
  color: var(--color-sand);
  width: 100%;
  text-align: left;
}

.hero-intro {
  opacity: 0; /* état initial pour GSAP */
  font-size: clamp(16px, 2vw, 20px);
  line-height: 1.7;
  max-width: 55ch;
  color: var(--color-sand-dim);
  margin-left: 4px;
}

/* Scroll indicator */
.scroll-indicator {
  position: absolute;
  bottom: 40px;
  left: 50%;
  transform: translateX(-50%);
  opacity: 0; /* état initial pour GSAP */
  display: flex;
  flex-direction: column;
  align-items: center;
}

.scroll-line {
  display: block;
  width: 1px;
  height: 64px;
  background: linear-gradient(to bottom, transparent, var(--color-sand-dim));
}

/* Responsive */
@media (max-width: 768px) {
  .hero-title {
    font-size: clamp(32px, 13vw, 96px);
    hyphens: auto;
    -webkit-hyphens: auto;
    overflow-wrap: break-word;
    word-break: break-word;
  }

  .hero-content {
    padding-top: 100px;
    gap: 20px;
  }
}
</style>
