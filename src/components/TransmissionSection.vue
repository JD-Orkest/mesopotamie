<script setup>
/**
 * TransmissionSection.vue
 * Section 3 : Chemins de Transmission — Gilles de Chin et le Crocodile.
 * Layout : texte à gauche (7 col) + image à droite (5 col), puis inversé.
 * GSAP : ligne de timeline animée + révélations au scroll.
 */
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const timelineRef = ref(null)
const baseUrl = import.meta.env.BASE_URL

onMounted(() => {
  if (!timelineRef.value) return

  // La ligne verticale de timeline se dessine au scroll
  gsap.fromTo(
    timelineRef.value.querySelector('.timeline-line'),
    { scaleY: 0 },
    {
      scaleY: 1,
      ease: 'none',
      scrollTrigger: {
        trigger: timelineRef.value,
        start: 'top 70%',
        end: 'bottom 30%',
        scrub: 1,
      },
    }
  )
})

const steps = [
  {
    id: 1,
    number: '01',
    label: 'Le Chaoskampf mésopotamien',
    date: '~1900 av. J.-C.',
    title: 'Marduk & Tiamat',
    body: 'Le motif du héros terrassant le dragon naît dans les plaines de Babylone. L\'Enuma Elish codifie le combat cosmique entre l\'ordre et le chaos. Ce schéma narratif rayonne depuis Babylone vers la Syrie, l\'Élam et le monde hellénistique.',
    imageSrc: 'https://oraedes.fr/Kirjasto/Ressources/Encyclopedie/Sculpture/Reliefs/Babylone_incn~bas-relief~Marduk-zakir-sumi-scribe.jpg',
    imageIntent: 'Bas-relief babylonien du dieu Marduk ou du dragon Mushkhushshu gardant la porte d\'Ishtar, éclairage dramatique',
    imageAlt: 'Dragon Mushkhushshu babylonien',
  },
  {
    id: 2,
    number: '02',
    label: 'Les Croisades — XIIe siècle',
    date: '~1130 apr. J.-C.',
    title: 'Gilles de Chin & la Pucelette',
    body: 'Gilles de Chin, chambellan du Hainaut et croisé, affronte un dragon dans les marais de Wasmes. Il ramène la Pucelette saine et sauve, et rapporte une tête de crocodile du Nil depuis la Terre Sainte — preuve physique du mythe, réalité zoologique. Les croisés rechargent le folklore européen des éléments de la zoologie mythique mésopotamienne.',
    imageSrc: `${baseUrl}images/transmission-2.png`,
    imageIntent: 'Chevalier médiéval en armure, scène de combat contre un dragon dans un marais (enluminure style médiéval sur fond sombre)',
    imageAlt: 'Gilles de Chin contre le Dragon de Wasmes',
    inverted: true,
  },
  {
    id: 3,
    number: '03',
    label: 'Le Trophée — Musée du Doudou',
    date: 'Attesté dès le XVe s.',
    title: 'La Tête de Crocodile',
    body: 'Le Musée du Doudou conserve une tête momifiée de crocodile du Nil. Pour la population médiévale du Hainaut, n\'ayant jamais vu de tels reptiles, cette tête curieuse était la preuve matérielle de l\'existence du dragon. L\'imagination populaire a transformé un animal exotique réel en une créature mythique, perpétuant la chaîne de transmission depuis Babylone.',
    imageSrc: `${baseUrl}images/transmission-3.png`,
    imageIntent: 'Tête momifiée de crocodile du Nil ou vitrine de musée archéologique, éclairage de galerie sombre',
    imageAlt: 'Tête de crocodile du Musée du Doudou',
  },
]
</script>

<template>
  <section id="transmission" class="transmission-section">
    <div class="container">

      <!-- En-tête -->
      <div class="section-header reveal">
        <span class="gold-line"></span>
        <p class="label-caps section-label">IV — Chemins de Transmission</p>
        <h2 class="section-title">Le Croisé & le Crocodile</h2>
        <p class="section-intro reveal">
          Le lien entre la Mésopotamie et le dragon de Mons ne relève pas de la filiation directe,
          mais d'une sédimentation de motifs narratifs traversant le Proche-Orient, filtrés par
          les Croisades, avant de s'enraciner dans le sol du Hainaut.
        </p>
      </div>

      <!-- Timeline des étapes de transmission -->
      <div ref="timelineRef" class="transmission-timeline">
        <!-- Ligne verticale animée -->
        <div class="timeline-line" aria-hidden="true"></div>

        <!-- Étapes -->
        <div
          v-for="step in steps"
          :key="step.id"
          :class="['timeline-step', { 'timeline-step--inverted': step.inverted }]"
        >
          <!-- Contenu textuel -->
          <div class="step-text reveal">
            <div class="step-number-wrapper">
              <span class="step-number label-caps">{{ step.number }}</span>
              <p class="label-caps step-label">{{ step.label }}</p>
            </div>
            <p class="label-caps step-date">{{ step.date }}</p>
            <h3 class="step-title">{{ step.title }}</h3>
            <p class="step-body">{{ step.body }}</p>
          </div>

          <!-- Point sur la ligne de timeline -->
          <div class="timeline-node" aria-hidden="true">
            <div class="node-dot"></div>
          </div>

          <!-- Image placeholder -->
          <div class="step-image reveal">
            <img
              v-if="step.imageSrc"
              class="step-image-img"
              :src="step.imageSrc"
              :alt="step.imageAlt"
              loading="lazy"
              referrerpolicy="no-referrer"
            />
            <div
              v-else
              class="img-placeholder"
              :data-image-intent="step.imageIntent"
            ></div>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>

<style scoped>
.transmission-section {
  padding: var(--section-gap) 0;
  overflow-x: clip;
}

/* ── En-tête ── */
.section-label {
  color: var(--color-gold);
  margin-bottom: 16px;
}

.section-title {
  font-size: var(--text-display-lg);
  letter-spacing: -0.02em;
  line-height: 1;
  margin-bottom: 32px;
}

.section-intro {
  font-size: var(--text-body-lg);
  max-width: 60ch;
  color: var(--color-sand-dim);
}

.section-header {
  margin-bottom: 80px;
}

/* ── Timeline ── */
.transmission-timeline {
  position: relative;
  display: flex;
  flex-direction: column;
  gap: 80px;
}

/* Ligne verticale centrale */
.timeline-line {
  position: absolute;
  left: 50%;
  top: 0;
  bottom: 0;
  width: 1px;
  background-color: var(--color-sand-ghost);
  transform-origin: top center;
  transform: scaleY(0);
}

@media (max-width: 900px) {
  .timeline-line {
    left: 0;
  }
}

/* ── Étape de timeline ── */
.timeline-step {
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  gap: 40px;
  align-items: center;
}

/* Version inversée : image à gauche, texte à droite */
.timeline-step--inverted .step-text {
  order: 3;
}

.timeline-step--inverted .timeline-node {
  order: 2;
}

.timeline-step--inverted .step-image {
  order: 1;
}

@media (max-width: 900px) {
  .timeline-step {
    grid-template-columns: auto 1fr;
    grid-template-rows: auto auto;
    column-gap: 16px;
    row-gap: 20px;
  }

  .timeline-step--inverted .step-text,
  .timeline-step--inverted .step-image {
    order: unset;
  }

  .timeline-node {
    grid-column: 1;
    grid-row: 1 / span 2;
    align-self: start;
    margin-top: 8px;
  }

  .step-text {
    grid-column: 2;
    grid-row: 1;
    min-width: 0;
  }

  .step-image {
    grid-column: 2;
    grid-row: 2;
    min-width: 0;
  }
}

/* ── Nœud de timeline ── */
.timeline-node {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-shrink: 0;
}

.node-dot {
  width: 12px;
  height: 12px;
  background-color: var(--color-gold);
  border: 2px solid var(--color-void);
  outline: 1px solid var(--color-gold);
}

/* ── Texte d'étape ── */
.step-number-wrapper {
  display: flex;
  align-items: center;
  gap: 16px;
  margin-bottom: 8px;
}

.step-number {
  font-size: 32px;
  font-family: var(--font-display);
  font-weight: 700;
  color: rgba(230, 223, 211, 0.10);
  letter-spacing: -0.02em;
  line-height: 1;
}

.step-label {
  color: var(--color-gold);
}

.step-date {
  color: rgba(230, 223, 211, 0.35);
  margin-bottom: 12px;
}

.step-title {
  font-size: clamp(24px, 3vw, 36px);
  font-weight: 600;
  margin-bottom: 16px;
  line-height: 1.2;
}

.step-body {
  font-size: var(--text-body-md);
  color: var(--color-sand-dim);
  line-height: 1.7;
  max-width: 50ch;
}

/* ── Image d'étape ── */
.step-image .img-placeholder {
  aspect-ratio: 4 / 3;
  width: 100%;
}

.step-image-img {
  aspect-ratio: 4 / 3;
  width: 100%;
  object-fit: cover;
  display: block;
}

@media (max-width: 600px) {
  .step-image-img,
  .step-image .img-placeholder {
    aspect-ratio: 16 / 10;
  }
}
</style>
