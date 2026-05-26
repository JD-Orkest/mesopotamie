<script setup>
/**
 * ChaoskampfSection.vue
 * Section 2 : Le Mythe du Chaoskampf — Marduk contre Tiamat.
 * Layout 2 colonnes asymétrique : image pivotée à gauche, texte à droite.
 * GSAP : parallaxe sur l'image au scroll + apparitions staggerées.
 */
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const sectionRef = ref(null)
const imageRef   = ref(null)
const img1Ref    = ref(null)
const img2Ref    = ref(null)
const baseUrl    = import.meta.env.BASE_URL

onMounted(() => {
  if (!sectionRef.value) return

  // Parallaxe : les deux images pivotées dérivent à des vitesses différentes
  gsap.to(img1Ref.value, {
    y: -80,
    ease: 'none',
    scrollTrigger: {
      trigger: sectionRef.value,
      start: 'top bottom',
      end: 'bottom top',
      scrub: 1.5,
    },
  })

  gsap.to(img2Ref.value, {
    y: -40,
    ease: 'none',
    scrollTrigger: {
      trigger: sectionRef.value,
      start: 'top bottom',
      end: 'bottom top',
      scrub: 1,
    },
  })
})
</script>

<template>
  <section id="chaoskampf" ref="sectionRef" class="chaoskampf-section">
    <div class="container">
      <div class="chaoskampf-grid">

        <!-- Colonne gauche : images superposées et pivotées -->
        <div ref="imageRef" class="chaos-image-col">
          <!-- Cadre bleu Lapis (décoratif) -->
          <div class="frame frame-lapis" aria-hidden="true"></div>

          <!-- Image principale pivotée -->
          <div ref="img1Ref" class="chaos-img chaos-img--main">
            <img
              class="chaos-photo"
              :src="`${baseUrl}images/tiamat-chaos.png`"
              alt="Tiamat, eaux primordiales en chaos"
              loading="lazy"
            />
          </div>

          <!-- Cadre or (décoratif) superposé -->
          <div class="frame frame-gold" aria-hidden="true"></div>

          <!-- Image secondaire décalée -->
          <div ref="img2Ref" class="chaos-img chaos-img--secondary">
            <img
              class="chaos-photo"
              :src="`${baseUrl}images/marduk-enuma.png`"
              alt="Tablette ou relief associe a Marduk"
              loading="lazy"
            />
          </div>
        </div>

        <!-- Colonne droite : texte éditorial -->
        <div class="chaos-text-col">
          <div class="chaos-text-inner">
            <span class="gold-line reveal"></span>
            <p class="label-caps chaos-label reveal">II — Enuma Elish</p>

            <h2 class="chaos-title reveal">
              La Lutte contre<br />
              le Chaos Primordial
            </h2>

            <p class="chaos-body reveal">
              Au cœur de la mythologie babylonienne réside l'Enuma Elish, une épopée
              relatant la création du monde à travers un combat violent. Marduk, le
              champion des dieux, affronte Tiamat, l'incarnation monstrueuse des eaux
              primordiales chaotiques.
            </p>

            <p class="chaos-body reveal">
              Ce récit — l'ordre terrassant le chaos — devient un motif fondateur.
              Le meurtre du serpent-dragon n'est pas seulement un mythe ; c'est un
              outil idéologique établissant la stabilité cosmique et politique.
              Marduk divise le cadavre de Tiamat en deux : d'une moitié, il façonne
              la voûte céleste ; de l'autre, la terre.
            </p>

            <!-- Citation mise en valeur -->
            <blockquote class="chaos-quote reveal">
              <p>
                « Il lui décoche une flèche qui lui transperce le cœur,
                mettant fin au règne du chaos. »
              </p>
              <cite class="label-caps">— Enuma Elish, tablette IV</cite>
            </blockquote>

            <!-- Table des caractéristiques du combat -->
            <div class="chaos-table-wrapper reveal">
              <table class="comparison-table">
                <thead>
                  <tr>
                    <th>Arme / Symbole</th>
                    <th>Signification cosmologique</th>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <td>Le filet et les vents</td>
                    <td>Contention et maîtrise de la force brute</td>
                  </tr>
                  <tr>
                    <td>Division du corps de Tiamat</td>
                    <td>Transformation du chaos en structure ordonnée</td>
                  </tr>
                  <tr>
                    <td>Le sang de Kingu</td>
                    <td>Création de l'humanité, servante de l'ordre divin</td>
                  </tr>
                  <tr>
                    <td>La fête de l'Akitu</td>
                    <td>Nécessité cyclique de régénérer le temps et la société</td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>

<style scoped>
.chaoskampf-section {
  padding: var(--section-gap) 0;
  overflow: hidden;
}

/* ── Grille asymétrique : 5 col image / 7 col texte ── */
.chaoskampf-grid {
  display: grid;
  grid-template-columns: 5fr 7fr;
  gap: var(--gutter);
  align-items: center;
  min-height: 720px;
}

@media (max-width: 900px) {
  .chaoskampf-grid {
    grid-template-columns: 1fr;
    gap: 60px;
  }
}

/* ── Colonne images ── */
.chaos-image-col {
  position: relative;
  min-height: 560px;
}

/* Image principale : pivotée légèrement */
.chaos-img {
  position: absolute;
  width: 75%;
  aspect-ratio: 1;
}

.chaos-img--main {
  top: 0;
  left: 0;
  transform: rotate(8deg);
  z-index: 2;
}

.chaos-img--secondary {
  bottom: 0;
  right: 0;
  transform: rotate(-5deg);
  z-index: 1;
  width: 65%;
}

.chaos-photo {
  aspect-ratio: 1;
  width: 100%;
  object-fit: cover;
  display: block;
}

/* Cadres décoratifs */
.frame {
  position: absolute;
  width: 72%;
  aspect-ratio: 1;
  z-index: 0;
  pointer-events: none;
}

.frame-lapis {
  top: -12px;
  left: -12px;
  border: 1px solid rgba(0, 79, 152, 0.6);
  transform: rotate(8deg);
}

.frame-gold {
  bottom: 16px;
  right: -8px;
  width: 60%;
  border: 1px solid rgba(212, 175, 55, 0.45);
  transform: rotate(-6deg);
  z-index: 3;
}

/* ── Colonne texte ── */
.chaos-text-col {
  display: flex;
  align-items: center;
}

.chaos-text-inner {
  max-width: 600px;
  padding-left: clamp(0px, 5vw, 64px);
}

.chaos-label {
  color: var(--color-gold);
  margin-bottom: 16px;
}

.chaos-title {
  font-size: var(--text-display-lg);
  font-weight: 600;
  line-height: 1.05;
  letter-spacing: -0.02em;
  margin-bottom: 32px;
}

.chaos-body {
  font-size: var(--text-body-lg);
  color: var(--color-sand-dim);
  line-height: 1.7;
  max-width: 55ch;
  margin-bottom: 24px;
}

/* Citation */
.chaos-quote {
  border-left: 2px solid var(--color-gold);
  padding-left: 24px;
  margin: 40px 0;
}

.chaos-quote p {
  font-family: var(--font-display);
  font-style: italic;
  font-size: clamp(16px, 2vw, 20px);
  line-height: 1.5;
  color: var(--color-sand);
  max-width: none;
  margin-bottom: 12px;
}

.chaos-quote cite {
  color: var(--color-gold);
}

/* Table */
.chaos-table-wrapper {
  margin-top: 8px;
  overflow-x: auto;
}

/* Responsive image col */
@media (max-width: 900px) {
  .chaos-image-col {
    min-height: 340px;
    order: 1;
  }

  .chaos-img--main {
    width: 60%;
  }

  .chaos-img--secondary {
    width: 50%;
  }

  .chaos-text-col {
    order: 2;
  }

  .chaos-text-inner {
    padding-left: 0;
  }
}
</style>
