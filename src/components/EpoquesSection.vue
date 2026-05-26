<script setup>
/**
 * EpoquesSection.vue
 * Section 1 : Les grandes époques de la Mésopotamie.
 * Cartes horizontalement scrollables (mobile) ou grille 3 colonnes (desktop).
 * GSAP : stagger d'entrée des cartes au scroll.
 */
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const sectionRef = ref(null)
const cardsRef   = ref(null)

const epoques = [
  {
    id: 'sumer',
    label: 'Sumer',
    date: '4100 – 2900 av. J.-C.',
    yearBig: '4500',
    title: 'Uruk & l\'Écriture Cunéiforme',
    body: 'L\'aube de l\'histoire enregistrée. L\'urbanisation, l\'invention de l\'écriture et les premières cités-États surgissant des plaines. Les Sumériens développent une cosmogonie où les forces de la nature doivent être domestiquées par le rite.',
    imageIntent: 'Tablette d\'argile cunéiforme sumérienne ou ziggurat d\'Uruk, fond sombre dramatique',
  },
  {
    id: 'akkad',
    label: 'Empire d\'Akkad',
    date: '2340 – 2180 av. J.-C.',
    yearBig: '2340',
    title: 'Sargon le Grand',
    body: 'L\'unification des cités-États en le premier véritable empire mondial. Un tournant de puissance, de langue, et de synthèse mythologique. Les dieux guerriers prennent une importance croissante dans un panthéon syncrétique.',
    imageIntent: 'Buste de Sargon d\'Akkad en bronze, éclairage dramatique, fond sombre',
  },
  {
    id: 'babylone',
    label: 'Empire Babylonien',
    date: '2004 – 1595 av. J.-C.',
    yearBig: '1800',
    title: 'Hammurabi & le Code des Lois',
    body: 'Loi, ordre, et la montée de Marduk. Hammurabi place le dieu au sommet du panthéon, faisant de sa victoire sur le chaos le mythe central de la civilisation mésopotamienne. Naissance de la jurisprudence mondiale.',
    imageIntent: 'Stèle du Code d\'Hammurabi ou représentation de Marduk/Babylone, éclairage dramatique',
  },
]

onMounted(() => {
  if (!cardsRef.value) return

  const cards = cardsRef.value.querySelectorAll('.epoch-card')

  gsap.fromTo(cards,
    { opacity: 0, y: 60 },
    {
      opacity: 1,
      y: 0,
      duration: 0.9,
      ease: 'power3.out',
      stagger: 0.15,
      scrollTrigger: {
        trigger: cardsRef.value,
        start: 'top 80%',
        once: true,
      },
    }
  )
})
</script>

<template>
  <section id="epoques" ref="sectionRef" class="epoques-section">
    <div class="container">
      <!-- En-tête de section -->
      <div class="section-header reveal">
        <span class="gold-line"></span>
        <p class="label-caps section-label">I — La Mésopotamie</p>
        <h2 class="section-title">Les Époques</h2>
        <p class="section-intro reveal">
          L'histoire de la Mésopotamie est celle de la naissance de la civilisation urbaine.
          Cette région — le « pays entre les fleuves » — a été le berceau d'innovations
          qui ont structuré la pensée humaine pour les millénaires à venir.
        </p>
      </div>

      <!-- Grille des cartes d'époques -->
      <div ref="cardsRef" class="epochs-grid">
        <article
          v-for="epoque in epoques"
          :key="epoque.id"
          class="epoch-card"
        >
          <!-- Placeholder image avec grand chiffre en surimpression -->
          <div class="card-image-wrapper">
            <!--
              ╔══════════════════════════════════════════════════╗
              ║  PLACEHOLDER IMAGE — Remplacez ce div par :     ║
              ║  <img src="/images/{{ epoque.id }}.jpg"         ║
              ║       :alt="epoque.title" />                     ║
              ╚══════════════════════════════════════════════════╝
            -->
            <div
              class="img-placeholder"
              :data-image-intent="epoque.imageIntent"
            ></div>
            <span class="card-year-bg" aria-hidden="true">{{ epoque.yearBig }}</span>
          </div>

          <!-- Contenu texte -->
          <div class="card-body">
            <p class="label-caps card-label">{{ epoque.label }}</p>
            <h3 class="card-title">{{ epoque.title }}</h3>
            <p class="card-text">{{ epoque.body }}</p>
            <p class="label-caps card-date">{{ epoque.date }}</p>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<style scoped>
.epoques-section {
  padding: var(--section-gap) 0;
  overflow-x: clip;
}

/* ── En-tête ── */
.section-header {
  margin-bottom: 64px;
}

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
  max-width: 55ch;
  color: var(--color-sand-dim);
}

/* ── Grille des cartes ── */
.epochs-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1px; /* ligne séparatrice subtile */
  background-color: var(--color-sand-ghost);
}

@media (max-width: 900px) {
  .epochs-grid {
    grid-template-columns: 1fr;
    gap: 1px;
  }
}

/* ── Carte individuelle ── */
.epoch-card {
  background-color: var(--color-void);
  display: flex;
  flex-direction: column;
  opacity: 0; /* état initial pour GSAP */
  transition: background 0.4s ease;
}

.epoch-card:hover {
  background-color: var(--color-surface);
}

/* Image */
.card-image-wrapper {
  position: relative;
  overflow: hidden;
}

.img-placeholder {
  aspect-ratio: 3 / 4;
  width: 100%;
}

/* Grand chiffre superposé */
.card-year-bg {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-family: var(--font-display);
  font-size: clamp(80px, 15vw, 160px);
  font-weight: 700;
  color: rgba(230, 223, 211, 0.08);
  letter-spacing: -0.04em;
  pointer-events: none;
  white-space: nowrap;
  transition: color 0.4s ease;
}

.epoch-card:hover .card-year-bg {
  color: rgba(230, 223, 211, 0.12);
}

/* Corps de carte */
.card-body {
  padding: 24px 24px 28px;
  display: flex;
  flex-direction: column;
  gap: 10px;
  flex: 1;
  border-top: 1px solid var(--color-sand-ghost);
}

.card-label {
  color: var(--color-gold);
  margin-bottom: 4px;
}

.card-title {
  font-size: clamp(22px, 2.5vw, 32px);
  font-weight: 600;
  letter-spacing: -0.01em;
  line-height: 1.2;
}

.card-text {
  font-size: var(--text-body-md);
  color: var(--color-sand-dim);
  line-height: 1.65;
  max-width: none;
  flex: 1;
}

.card-date {
  margin-top: 8px;
  color: rgba(230, 223, 211, 0.35);
}
</style>
