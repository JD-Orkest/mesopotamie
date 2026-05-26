<script setup>
/**
 * AnatomieSection.vue
 * Section 5 : Anatomie du Lumeçon — acteurs, symbolique, théorie des couleurs.
 * Layout : grande grille de personnages + focus sur le Dragon.
 * GSAP : cartes qui s'élèvent au scroll + texte anatomique révélé.
 */
import { onMounted, onUnmounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const cardsRef       = ref(null)
const dragonRef      = ref(null)
const selectedActeur = ref(null)

function openModal(acteur) {
  selectedActeur.value = acteur
  document.body.style.overflow = 'hidden'
}

function closeModal() {
  selectedActeur.value = null
  document.body.style.overflow = ''
}

function onKeydown(e) {
  if (e.key === 'Escape') closeModal()
}

onUnmounted(() => {
  document.removeEventListener('keydown', onKeydown)
  document.body.style.overflow = ''
})

onMounted(() => {
  document.addEventListener('keydown', onKeydown)

  if (cardsRef.value) {
    const cards = cardsRef.value.querySelectorAll('.actor-card')
    gsap.fromTo(cards,
      { opacity: 0, y: 50 },
      {
        opacity: 1,
        y: 0,
        duration: 0.8,
        ease: 'power3.out',
        stagger: 0.12,
        scrollTrigger: {
          trigger: cardsRef.value,
          start: 'top 80%',
          once: true,
        },
      }
    )
  }

  if (dragonRef.value) {
    gsap.fromTo(dragonRef.value,
      { opacity: 0, scale: 0.97 },
      {
        opacity: 1,
        scale: 1,
        duration: 1.2,
        ease: 'power3.out',
        scrollTrigger: {
          trigger: dragonRef.value,
          start: 'top 80%',
          once: true,
        },
      }
    )
  }
})

const acteurs = [
  {
    id: 'saint-georges',
    label: 'Saint Georges',
    role: 'Héros civilisateur, garant de l\'ordre',
    symbolisme: 'Continuité, identité et ordre social',
    costume: 'Armure, costume jaune et bleu, lances, pistolet',
    couleur: '#D4AF37',
    colorLabel: 'Jaune & Bleu',
    imageIntent: 'Saint Georges en armure, costume jaune et bleu, tenant une lance, style médiéval sur fond sombre',
    bodyText: 'Saint Georges, martyr du IVe siècle originaire de Cappadoce, est devenu le parfait réceptacle du rôle de chevalier céleste. Il incarne la continuité, l\'identité et l\'ordre, faisant écho à Marduk combattant pour instaurer la loi cosmique.',
  },
  {
    id: 'dragon',
    label: 'El Biète — Le Dragon',
    role: 'Force du désordre et du changement',
    symbolisme: 'Chaos nécessaire, gardien du seuil',
    costume: '10 mètres de long, vert, queue en crin de cheval',
    couleur: '#2E7D32',
    colorLabel: 'Vert & Noir',
    imageIntent: 'Dragon de la Ducasse de Mons — grande structure articulée verte, défilé festif, foule qui arrache le crin',
    bodyText: 'Le Dragon n\'est pas complètement mauvais, ni complètement bon. Il est une force nécessaire du changement. Comme Tiamat, dont le corps est le matériau même du monde, il est une partie indissociable de la totalité.',
  },
  {
    id: 'chinchins',
    label: 'Les Chinchins',
    role: 'Chiens protecteurs, alliés de Saint Georges',
    symbolisme: 'Animalité domestiquée au service de l\'ordre',
    costume: 'Veste tartan rouge, chevaux-jupons en osier',
    couleur: '#B71C1C',
    colorLabel: 'Rouge',
    imageIntent: 'Les Chinchins en costume rouge tartan, montés sur leurs chevaux en osier, Ducasse de Mons',
    bodyText: 'Comme Marduk associé au Mushkhushshu après sa victoire, les Chinchins représentent l\'animalité domestiquée et fidèle. Ils mordent le museau du dragon et attaquent les Diables, participant à la neutralisation du chaos.',
  },
  {
    id: 'hommes-feuilles',
    label: 'Les Hommes de Feuilles',
    role: 'Protecteurs de la queue du dragon',
    symbolisme: 'Lien primitif avec la nature, écho d\'Enkidu',
    costume: 'Tenue couverte de feuilles de lierre, massues',
    couleur: '#33691E',
    colorLabel: 'Vert sauvage',
    imageIntent: 'Hommes de Feuilles du Lumeçon — costumes couverts de lierre, portant la queue du dragon, atmosph ère sauvage',
    bodyText: 'Ils renvoient irrésistiblement à Enkidu dans l\'Épopée de Gilgamesh. Comme lui, les Hommes de Feuilles représentent ce lien primitif avec la terre que la civilisation doit intégrer pour s\'épanouir.',
  },
  {
    id: 'diables',
    label: 'Les Diables',
    role: 'Alliés du dragon, fauteurs de troubles',
    symbolisme: 'Forces anarchiques, désordre incarné',
    costume: 'Salopette noire, cornes rouges, vessies de porc',
    couleur: '#1A1A1A',
    colorLabel: 'Noir & Rouge',
    imageIntent: 'Les Diables du Lumeçon en salopette noire avec cornes rouges, maquillage dramatique, agitant des vessies',
    bodyText: 'Les Diables s\'inscrivent dans la structure binaire ordre/désordre, blanc/noir, au cœur de la pensée mésopotamienne. Comme les agents de Tiamat, ils servent la cause du désordre avant que l\'ordre ne triomphe.',
  },
  {
    id: 'hommes-blancs',
    label: 'Les Hommes Blancs',
    role: 'Porteurs du dragon, garants de l\'équilibre',
    symbolisme: 'Neutralité cosmique, équilibre des forces',
    costume: 'Entièrement vêtus de blanc, ceinture noire',
    couleur: '#E6DFD3',
    colorLabel: 'Blanc & Noir',
    imageIntent: 'Les Hommes Blancs en costume entièrement blanc portant le corps du dragon, Ducasse de Mons',
    bodyText: 'La théorie de l\'inversion des couleurs : Hommes Blancs en blanc avec touches de noir, Diables en noir avec touches de blanc. Cette structure chromatique réactive le principe d\'équilibre nécessaire à la marche du monde.',
  },
]

const dragonAnatomy = [
  { label: 'Longueur',   value: 'Environ 10 mètres',            detail: 'Rappelle la taille colossale des monstres primordiaux babyloniens' },
  { label: 'Couleur',    value: 'Vert (nature) + nageoires noires', detail: 'Couleur naturante symbolisant la vie, la fertilité et les profondeurs' },
  { label: 'Matériaux',  value: 'Osier, toile peinte, fibre de carbone', detail: 'Évolution des techniques de fabrication des géants processionnels' },
  { label: 'Queue',      value: 'Crin de cheval, portée par 8 Hommes de Feuilles', detail: 'Symbole de puissance et de lien cosmique avec la terre' },
  { label: 'Dents',      value: 'Convoitées par le public comme trophées', detail: 'Vestige du dépeçage rituel du monstre vaincu (écho de Tiamat)' },
]
</script>

<template>
  <section id="anatomie" class="anatomie-section">
    <div class="container">

      <!-- En-tête -->
      <div class="section-header reveal">
        <span class="gold-line"></span>
        <p class="label-caps section-label">VI — Le Lumeçon</p>
        <h2 class="section-title">Anatomie du Combat</h2>
        <p class="section-intro reveal">
          Chaque acteur du Lumeçon porte un héritage symbolique dont les couches
          de signification remontent à l'antiquité mésopotamienne. L'influence
          de Babylone transparaît dans la structure binaire ordre/désordre
          et dans la caractérisation de chaque personnage.
        </p>
      </div>

      <!-- Grille des acteurs -->
      <div ref="cardsRef" class="actors-grid">
        <article
          v-for="acteur in acteurs"
          :key="acteur.id"
          class="actor-card"
          role="button"
          tabindex="0"
          :aria-label="'Voir la fiche complète de ' + acteur.label"
          @click="openModal(acteur)"
          @keydown.enter="openModal(acteur)"
          @keydown.space.prevent="openModal(acteur)"
        >
          <!-- Bande couleur en haut de la carte -->
          <div
            class="card-color-band"
            :style="{ backgroundColor: acteur.couleur }"
            aria-hidden="true"
          ></div>

          <!-- Image placeholder -->
          <div class="actor-image">
            <!--
              ╔══════════════════════════════════════════════════════════╗
              ║  PLACEHOLDER IMAGE — Remplacez ce div par :              ║
              ║  <img src="/images/{{ acteur.id }}.jpg"                  ║
              ║       :alt="acteur.label" />                             ║
              ╚══════════════════════════════════════════════════════════╝
            -->
            <div
              class="img-placeholder"
              :data-image-intent="acteur.imageIntent"
            ></div>
          </div>

          <!-- Contenu -->
          <div class="actor-body">
            <p class="label-caps actor-label">{{ acteur.label }}</p>
            <p class="label-caps actor-color-label" :style="{ color: acteur.couleur }">
              {{ acteur.colorLabel }}
            </p>
            <p class="actor-role">{{ acteur.role }}</p>
            <p class="actor-text">{{ acteur.bodyText }}</p>
            <div class="actor-footer">
              <span class="label-caps actor-costume-label">Costume</span>
              <p class="actor-costume">{{ acteur.costume }}</p>
            </div>
            <!-- Indicateur pointillé -->
            <span class="actor-hint label-caps" aria-hidden="true">· · · Voir la fiche</span>
          </div>
        </article>
      </div>

      <!-- Modal acteur -->
      <Teleport to="body">
        <Transition name="modal">
          <div
            v-if="selectedActeur"
            class="actor-modal-backdrop"
            @click.self="closeModal"
            role="dialog"
            :aria-label="selectedActeur.label"
            aria-modal="true"
          >
            <div class="actor-modal">

              <!-- Fermeture -->
              <button class="modal-close" @click="closeModal" aria-label="Fermer">
                <span aria-hidden="true">✕</span>
              </button>

              <!-- Bande couleur haut -->
              <div
                class="modal-color-band"
                :style="{ backgroundColor: selectedActeur.couleur }"
                aria-hidden="true"
              ></div>

              <div class="modal-inner">

                <!-- Image -->
                <div class="modal-image">
                  <div
                    class="img-placeholder modal-img-placeholder"
                    :data-image-intent="selectedActeur.imageIntent"
                  ></div>
                </div>

                <!-- Contenu complet -->
                <div class="modal-content">
                  <p class="label-caps modal-color-label" :style="{ color: selectedActeur.couleur }">
                    {{ selectedActeur.colorLabel }}
                  </p>
                  <h3 class="modal-title">{{ selectedActeur.label }}</h3>
                  <p class="label-caps modal-role-label">Rôle dans le Lumeçon</p>
                  <p class="modal-role">{{ selectedActeur.role }}</p>
                  <p class="modal-body">{{ selectedActeur.bodyText }}</p>

                  <div class="modal-details">
                    <div class="modal-detail-item">
                      <span class="label-caps modal-detail-label">Symbolisme</span>
                      <p class="modal-detail-value">{{ selectedActeur.symbolisme }}</p>
                    </div>
                    <div class="modal-detail-item">
                      <span class="label-caps modal-detail-label">Costume</span>
                      <p class="modal-detail-value">{{ selectedActeur.costume }}</p>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </Transition>
      </Teleport>

      <!-- Section focus : Anatomie du Dragon -->
      <div ref="dragonRef" class="dragon-focus">
        <div class="dragon-focus-grid">

          <!-- Image principale du Dragon -->
          <div class="dragon-image-col">
            <!--
              ╔══════════════════════════════════════════════════════════╗
              ║  PLACEHOLDER IMAGE                                       ║
              ║  Intent : Gros plan sur la tête du Dragon de Mons,       ║
              ║  bouche ouverte, dents visibles, éclairage dramatique.   ║
              ║  Remplacez par :                                         ║
              ║  <img src="/images/dragon-gros-plan.jpg" alt="Dragon" />  ║
              ╚══════════════════════════════════════════════════════════╝
            -->
            <div
              class="img-placeholder dragon-main-img"
              data-image-intent="Gros plan tête du Dragon du Lumeçon de Mons, gueule ouverte avec dents, éclairage dramatique et sombre"
            ></div>
          </div>

          <!-- Tableau anatomique -->
          <div class="dragon-text-col">
            <span class="gold-line"></span>
            <p class="label-caps dragon-label">Anatomie de la « Biète »</p>
            <h3 class="dragon-title">El Biète — Portrait du Dragon</h3>
            <p class="dragon-intro">
              Contrairement à une vision purement négative, le folklore montois
              voit en lui un gardien. Le dragon garde l'entrée vers la richesse
              intérieure et la connaissance. Sans le combat, il n'y a pas de
              renouveau pour Mons — sans la défaite de Tiamat, pas de création.
            </p>

            <table class="comparison-table dragon-table">
              <thead>
                <tr>
                  <th>Caractéristique</th>
                  <th>Détail</th>
                  <th>Analogie mésopotamienne</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="item in dragonAnatomy" :key="item.label">
                  <td>{{ item.label }}</td>
                  <td>{{ item.value }}</td>
                  <td>{{ item.detail }}</td>
                </tr>
              </tbody>
            </table>
          </div>

        </div>
      </div>

      <!-- Conclusion éditoriale -->
      <div class="conclusion reveal">
        <p class="label-caps conclusion-label">IX — Conclusion</p>
        <blockquote class="conclusion-quote">
          <p>
            La queue du dragon, que les Montois s'arrachent, est le lien physique
            qui unit encore les citoyens de Mons aux bâtisseurs de ziggurats.
            Lorsque la foule scande « Et les Montois ne périront pas ! », elle réitère
            sans le savoir la promesse faite par Marduk sur les eaux de l'Euphrate :
            celle que tant que l'homme saura affronter son dragon, la civilisation
            perdurera.
          </p>
        </blockquote>
      </div>

    </div>
  </section>
</template>

<style scoped>
.anatomie-section {
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
  margin-bottom: 64px;
}

/* ── Grille acteurs ── */
.actors-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1px;
  background-color: var(--color-sand-ghost);
  margin-bottom: 80px;
}

@media (max-width: 900px) {
  .actors-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 520px) {
  .actors-grid {
    grid-template-columns: 1fr;
    gap: 0;
  }
}

/* ── Carte acteur ── */
.actor-card {
  background-color: var(--color-void);
  display: flex;
  flex-direction: column;
  opacity: 0; /* état initial GSAP */
  position: relative;
  transition: background 0.3s ease;
  cursor: pointer;
}

.actor-card:hover {
  background-color: var(--color-surface);
}

/* Indicateur pointillé bas de carte */
.actor-hint {
  display: block;
  margin-top: 12px;
  font-size: 9px;
  letter-spacing: 0.18em;
  color: rgba(212, 175, 55, 0);
  border-top: 1px dashed rgba(212, 175, 55, 0);
  padding-top: 10px;
  transition: color 0.3s ease, border-color 0.3s ease;
}

.actor-card:hover .actor-hint,
.actor-card:focus-visible .actor-hint {
  color: rgba(212, 175, 55, 0.7);
  border-color: rgba(212, 175, 55, 0.3);
}

/* Sur écran tactile (pas de hover) : toujours visible */
@media (hover: none) {
  .actor-hint {
    color: rgba(212, 175, 55, 0.55);
    border-color: rgba(212, 175, 55, 0.2);
  }
}

.actor-card:focus-visible {
  outline: 1px dashed rgba(212, 175, 55, 0.5);
  outline-offset: -2px;
}

.card-color-band {
  height: 3px;
  width: 100%;
  opacity: 0.7;
}

.actor-image .img-placeholder {
  aspect-ratio: 3 / 4;
}

.actor-body {
  padding: 20px 20px 24px;
  display: flex;
  flex-direction: column;
  gap: 8px;
  flex: 1;
  border-top: 1px solid var(--color-sand-ghost);
}

.actor-label {
  color: var(--color-sand);
  font-size: 10px;
}

.actor-color-label {
  font-size: 10px;
  margin-top: -4px;
}

.actor-role {
  font-size: 13px;
  font-weight: 600;
  color: var(--color-sand);
  font-family: var(--font-display);
  font-style: italic;
  line-height: 1.3;
  max-width: none;
}

.actor-text {
  font-size: 14px;
  color: var(--color-sand-dim);
  line-height: 1.65;
  max-width: none;
  flex: 1;
}

.actor-footer {
  margin-top: 8px;
  padding-top: 12px;
  border-top: 1px solid var(--color-sand-ghost);
}

/* ── Cartes horizontales sur mobile ── */
@media (max-width: 520px) {
  .actor-card {
    flex-direction: row;
    align-items: stretch;
    border-bottom: 1px solid var(--color-sand-ghost);
  }

  .card-color-band {
    width: 4px;
    height: auto;
    flex-shrink: 0;
  }

  .actor-image {
    flex-shrink: 0;
    width: 88px;
  }

  .actor-image .img-placeholder {
    aspect-ratio: unset;
    width: 88px;
    height: 100%;
  }

  .actor-body {
    border-top: none;
    border-left: 1px solid var(--color-sand-ghost);
    padding: 14px 14px 16px;
    gap: 5px;
    justify-content: center;
  }

  .actor-text {
    display: -webkit-box;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
    overflow: hidden;
    font-size: 13px;
  }

  .actor-footer {
    display: none;
  }

  .actor-hint {
    margin-top: 8px;
    padding-top: 8px;
  }
}

.actor-costume-label {
  color: var(--color-gold);
  margin-bottom: 4px;
  display: block;
}

.actor-costume {
  font-size: 13px;
  color: rgba(230, 223, 211, 0.45);
  max-width: none;
  line-height: 1.5;
}

/* ── Focus Dragon ── */
.dragon-focus {
  opacity: 0; /* état initial GSAP */
  margin-bottom: 80px;
}

.dragon-focus-grid {
  display: grid;
  grid-template-columns: 5fr 7fr;
  gap: 64px;
  align-items: start;
}

@media (max-width: 900px) {
  .dragon-focus-grid {
    grid-template-columns: 1fr;
    gap: 40px;
  }
}

.dragon-main-img {
  aspect-ratio: 3 / 4;
  width: 100%;
}

@media (max-width: 900px) {
  .dragon-main-img {
    aspect-ratio: 16 / 9;
  }
}

.dragon-label {
  color: var(--color-gold);
  margin-bottom: 12px;
}

.dragon-title {
  font-size: clamp(24px, 3vw, 36px);
  font-weight: 600;
  margin-bottom: 20px;
  line-height: 1.2;
}

.dragon-intro {
  font-size: var(--text-body-md);
  color: var(--color-sand-dim);
  line-height: 1.7;
  max-width: none;
  margin-bottom: 32px;
}

.dragon-table {
  font-size: 14px;
}

/* Masquer la colonne analogie sur mobile — trop large à 3 colonnes */
@media (max-width: 640px) {
  .dragon-table thead tr th:last-child,
  .dragon-table tbody tr td:last-child {
    display: none;
  }

  .dragon-intro {
    font-size: 14px;
  }
}

/* ── Conclusion ── */
.conclusion {
  border-top: 1px solid var(--color-sand-ghost);
  padding-top: 80px;
  margin-top: 40px;
}

.conclusion-label {
  color: var(--color-gold);
  margin-bottom: 24px;
}

.conclusion-quote {
  max-width: 75ch;
}

.conclusion-quote p {
  font-family: var(--font-display);
  font-size: clamp(18px, 2.5vw, 28px);
  font-style: italic;
  line-height: 1.5;
  color: var(--color-sand);
  max-width: none;
}

/* ══════════════════════════════════════════════
   Modal acteur
   ══════════════════════════════════════════════ */

/* Transition d'entrée/sortie */
.modal-enter-active,
.modal-leave-active {
  transition: opacity 0.3s ease;
}
.modal-enter-active .actor-modal {
  transition: transform 0.35s cubic-bezier(0.16, 1, 0.3, 1), opacity 0.3s ease;
}
.modal-leave-active .actor-modal {
  transition: transform 0.25s ease-in, opacity 0.25s ease-in;
}
.modal-enter-from,
.modal-leave-to {
  opacity: 0;
}
.modal-enter-from .actor-modal {
  transform: translateY(32px);
  opacity: 0;
}
.modal-leave-to .actor-modal {
  transform: translateY(16px);
  opacity: 0;
}

/* Fond sombre */
.actor-modal-backdrop {
  position: fixed;
  inset: 0;
  z-index: 1000;
  background: rgba(15, 17, 21, 0.88);
  backdrop-filter: blur(6px);
  -webkit-backdrop-filter: blur(6px);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 24px 16px;
  overflow-y: auto;
}

/* Fenêtre modale */
.actor-modal {
  position: relative;
  background: #191c22;
  border: 1px solid var(--color-sand-ghost);
  width: 100%;
  max-width: 860px;
  max-height: calc(100dvh - 48px);
  overflow-y: auto;
  border-radius: 2px;
}

/* Bande couleur en haut */
.modal-color-band {
  height: 4px;
  width: 100%;
  opacity: 0.85;
}

/* Bouton fermeture */
.modal-close {
  position: sticky;
  top: 0;
  float: right;
  z-index: 10;
  background: rgba(15, 17, 21, 0.7);
  border: 1px solid var(--color-sand-ghost);
  color: var(--color-sand);
  font-size: 18px;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  margin: 12px 12px 0 0;
  transition: background 0.2s ease, border-color 0.2s ease;
}
.modal-close:hover {
  background: var(--color-surface);
  border-color: var(--color-gold);
}

/* Layout intérieur : image + texte */
.modal-inner {
  display: grid;
  grid-template-columns: 5fr 7fr;
  gap: 0;
  clear: both;
}

@media (max-width: 640px) {
  .modal-inner {
    grid-template-columns: 1fr;
  }
}

/* Image dans le modal */
.modal-image {
  position: relative;
}

.modal-img-placeholder {
  aspect-ratio: 3 / 4;
  width: 100%;
  height: 100%;
}

@media (max-width: 640px) {
  .modal-img-placeholder {
    aspect-ratio: 4 / 3;
  }
}

/* Contenu textuel */
.modal-content {
  padding: 32px 28px 36px;
  border-left: 1px solid var(--color-sand-ghost);
}

@media (max-width: 640px) {
  .modal-content {
    border-left: none;
    border-top: 1px solid var(--color-sand-ghost);
    padding: 24px 20px 28px;
  }
}

.modal-color-label {
  font-size: 10px;
  margin-bottom: 8px;
}

.modal-title {
  font-size: clamp(22px, 3.5vw, 34px);
  font-weight: 700;
  line-height: 1.1;
  margin-bottom: 20px;
  color: var(--color-sand);
}

.modal-role-label {
  color: var(--color-gold);
  font-size: 9px;
  margin-bottom: 6px;
}

.modal-role {
  font-family: var(--font-display);
  font-style: italic;
  font-size: 15px;
  color: var(--color-sand);
  margin-bottom: 16px;
  max-width: none;
  line-height: 1.4;
}

.modal-body {
  font-size: 15px;
  color: var(--color-sand-dim);
  line-height: 1.75;
  max-width: none;
  margin-bottom: 28px;
}

.modal-details {
  display: flex;
  flex-direction: column;
  gap: 16px;
  padding-top: 20px;
  border-top: 1px dashed rgba(230, 223, 211, 0.15);
}

.modal-detail-label {
  display: block;
  color: var(--color-gold);
  font-size: 9px;
  margin-bottom: 4px;
}

.modal-detail-value {
  font-size: 13px;
  color: rgba(230, 223, 211, 0.55);
  max-width: none;
  line-height: 1.5;
}
</style>
