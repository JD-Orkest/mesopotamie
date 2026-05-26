<script setup>
/**
 * RituelsSection.vue
 * Section 4 : Les Rituels — Akitu de Babylone & Ducasse de Mons.
 * Layout : tableau comparatif + présentation des 4 temps forts du Doudou.
 * GSAP : apparitions staggerées des lignes du tableau au scroll.
 */
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const tableRef = ref(null)
const momentsRef = ref(null)

onMounted(() => {
  if (tableRef.value) {
    const rows = tableRef.value.querySelectorAll('tbody tr')
    gsap.fromTo(rows,
      { opacity: 0, x: -20 },
      {
        opacity: 1,
        x: 0,
        duration: 0.6,
        ease: 'power2.out',
        stagger: 0.1,
        scrollTrigger: {
          trigger: tableRef.value,
          start: 'top 85%',
          once: true,
        },
      }
    )
  }

  if (momentsRef.value) {
    const items = momentsRef.value.querySelectorAll('.moment-item')
    gsap.fromTo(items,
      { opacity: 0, y: 30 },
      {
        opacity: 1,
        y: 0,
        duration: 0.8,
        ease: 'power3.out',
        stagger: 0.15,
        scrollTrigger: {
          trigger: momentsRef.value,
          start: 'top 80%',
          once: true,
        },
      }
    )
  }
})

const comparaison = [
  {
    element: 'Objectif Central',
    akitu: 'Régénérer l\'ordre cosmique et politique',
    doudou: 'Assurer la survie et l\'identité de la cité',
  },
  {
    element: 'Figure Héroïque',
    akitu: 'Marduk (dieu de l\'orage et roi des dieux)',
    doudou: 'Saint Georges (chevalier chrétien et martyr)',
  },
  {
    element: 'Antagoniste',
    akitu: 'Tiamat (monstre marin, chaos primordial)',
    doudou: 'Le Dragon — symbole de désordre et de changement',
  },
  {
    element: 'Moment Critique',
    akitu: 'Gifle au roi (si pleurs, Marduk est apaisé)',
    doudou: 'Montée du Car d\'Or (réussite = année faste)',
  },
  {
    element: 'Action de la Foule',
    akitu: 'Accompagnement de la procession divine',
    doudou: 'Arracher le crin de la queue du dragon',
  },
  {
    element: 'Résultat Final',
    akitu: 'Fixation des destinées pour l\'année',
    doudou: '"Et les Montois ne périront pas !"',
  },
]

const moments = [
  {
    num: '01',
    title: 'La Descente de la Châsse',
    timing: 'Samedi soir',
    body: 'Les reliques de Sainte Waudru sont descendues de leur autel dans la collégiale et confiées aux autorités civiles. Le public chante l\'air du Doudou, scellant l\'union entre la sainte protectrice et les citoyens.',
    imageIntent: 'Intérieur de la Collégiale Sainte-Waudru de Mons, lumières de cierges, châsse dorée en procession',
  },
  {
    num: '02',
    title: 'La Procession du Car d\'Or',
    timing: 'Dimanche matin',
    body: 'La châsse est placée sur un char monumental tiré par six chevaux de trait. Des centaines de figurants reconstituent les confréries et corporations médiévales, défilant dans les rues de la ville.',
    imageIntent: 'Car d\'Or — char monumental doré tiré par des chevaux, en procession dans les rues de Mons',
  },
  {
    num: '03',
    title: 'La Montée du Car d\'Or',
    timing: 'Dimanche midi',
    body: 'Le char doit gravir d\'un seul élan la rampe pavée menant à la collégiale. La foule se masse derrière le char pour le pousser. Si le char échoue à monter, le malheur s\'abattra sur la ville.',
    imageIntent: 'Foule dense poussant le Car d\'Or dans la montée pavée de Mons, tension dramatique',
  },
  {
    num: '04',
    title: 'Le Combat dit Lumeçon',
    timing: 'Dimanche après-midi',
    body: 'Sur la Grand-Place, Saint Georges affronte le Dragon devant des milliers de spectateurs. Le public participe activement en tentant d\'arracher le crin de la queue du monstre — et les Montois ne périront pas !',
    imageIntent: 'Combat du Lumeçon — Saint Georges en costume jaune face au Dragon vert sur la Grand-Place de Mons, foule en délire',
  },
]
</script>

<template>
  <section id="rituels" class="rituels-section">
    <div class="container">

      <!-- En-tête -->
      <div class="section-header reveal">
        <span class="gold-line"></span>
        <p class="label-caps section-label">III & V — Akitu & Doudou</p>
        <h2 class="section-title">Les Rituels</h2>
      </div>

      <!-- Deux colonnes : intro + image Ducasse -->
      <div class="rituels-intro-grid">
        <div class="rituels-intro-text">
          <p class="reveal">
            La comparaison entre l'Akitu de Babylone et la Ducasse de Mons révèle
            des analogies structurelles profondes. L'Akitu célébrait le Nouvel An
            babylonien — un moment de passage où l'univers risquait de retourner
            au chaos si les rites n'étaient pas accomplis. Durant douze jours,
            la ville de Babylone devenait le théâtre de rites complexes visant
            à assurer la fertilité et l'ordre pour l'année à venir.
          </p>
          <p class="reveal">
            À Mons, la Ducasse de Mons — le Doudou — fixée au dimanche de la
            Trinité depuis 1349, partage cette même structure rituelle.
            Le cri « Et les Montois ne périront pas ! » est l'expression
            d'un renouveau vital, assurant la survie de la communauté
            pour l'année suivante.
          </p>
        </div>

        <div class="rituels-intro-image reveal">
          <!--
            ╔══════════════════════════════════════════════════════════╗
            ║  PLACEHOLDER IMAGE                                       ║
            ║  Intent : Vue aérienne de la Grand-Place de Mons         ║
            ║  pendant la Ducasse, foule immense, atmosphère festive.  ║
            ║  Remplacez par :                                         ║
            ║  <img src="/images/ducasse-grand-place.jpg"              ║
            ║       alt="La Ducasse de Mons" />                        ║
            ╚══════════════════════════════════════════════════════════╝
          -->
          <div
            class="img-placeholder"
            data-image-intent="Vue aérienne de la Grand-Place de Mons pendant la Ducasse, foule, Car d'Or, ambiance festive"
          ></div>
        </div>
      </div>

      <!-- Tableau comparatif Akitu / Doudou -->
      <div class="table-section">
        <h3 class="table-title reveal">Akitu de Babylone / Ducasse de Mons</h3>
        <div class="table-wrapper reveal" ref="tableRef">
          <table class="comparison-table">
            <thead>
              <tr>
                <th>Élément</th>
                <th>Festival Akitu (Babylone)</th>
                <th>Ducasse de Mons (Doudou)</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="row in comparaison" :key="row.element">
                <td>{{ row.element }}</td>
                <td>{{ row.akitu }}</td>
                <td>{{ row.doudou }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>

      <!-- Les 4 temps forts du Doudou -->
      <div class="moments-section">
        <h3 class="table-title reveal">Les quatre temps forts du Doudou</h3>
        <div ref="momentsRef" class="moments-grid">
          <article
            v-for="moment in moments"
            :key="moment.num"
            class="moment-item"
          >
            <div class="moment-image">
              <!--
                ╔══════════════════════════════════════════════════════╗
                ║  PLACEHOLDER IMAGE — Remplacez ce div par :          ║
                ║  <img src="/images/moment-{{ moment.num }}.jpg"      ║
                ║       :alt="moment.title" />                          ║
                ╚══════════════════════════════════════════════════════╝
              -->
              <div
                class="img-placeholder"
                :data-image-intent="moment.imageIntent"
              ></div>
            </div>

            <div class="moment-body">
              <div class="moment-header">
                <span class="moment-num label-caps">{{ moment.num }}</span>
                <span class="moment-timing label-caps">{{ moment.timing }}</span>
              </div>
              <h4 class="moment-title">{{ moment.title }}</h4>
              <p class="moment-text">{{ moment.body }}</p>
            </div>
          </article>
        </div>
      </div>

    </div>
  </section>
</template>

<style scoped>
.rituels-section {
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
  margin-bottom: 0;
}

.section-header {
  margin-bottom: 64px;
}

/* ── Grille intro (texte + image) ── */
.rituels-intro-grid {
  display: grid;
  grid-template-columns: 7fr 5fr;
  gap: 64px;
  align-items: start;
  margin-bottom: 80px;
}

@media (max-width: 900px) {
  .rituels-intro-grid {
    grid-template-columns: 1fr;
    gap: 40px;
  }
}

.rituels-intro-text {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.rituels-intro-text p {
  font-size: var(--text-body-lg);
  color: var(--color-sand-dim);
  max-width: none;
}

.rituels-intro-image .img-placeholder {
  aspect-ratio: 4 / 5;
}

/* ── Table section ── */
.table-section {
  margin-bottom: 80px;
}

.table-title {
  font-size: clamp(20px, 2.5vw, 28px);
  font-weight: 500;
  margin-bottom: 24px;
  color: var(--color-sand);
}

.table-wrapper {
  overflow-x: auto;
}

/* ── 4 Moments du Doudou ── */
.moments-section {
  margin-top: 80px;
}

.moments-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1px;
  background-color: var(--color-sand-ghost);
}

@media (max-width: 700px) {
  .moments-grid {
    grid-template-columns: 1fr;
  }
}

.moment-item {
  background-color: var(--color-void);
  display: flex;
  flex-direction: column;
  opacity: 0; /* état initial GSAP */
  transition: background 0.3s ease;
}

.moment-item:hover {
  background-color: var(--color-surface);
}

.moment-image .img-placeholder {
  aspect-ratio: 16 / 9;
}

.moment-body {
  padding: 24px;
  display: flex;
  flex-direction: column;
  gap: 10px;
  border-top: 1px solid var(--color-sand-ghost);
  flex: 1;
}

.moment-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.moment-num {
  color: var(--color-gold);
}

.moment-timing {
  color: rgba(230, 223, 211, 0.35);
}

.moment-title {
  font-size: clamp(18px, 2vw, 24px);
  font-weight: 600;
  line-height: 1.3;
}

.moment-text {
  font-size: var(--text-body-md);
  color: var(--color-sand-dim);
  line-height: 1.65;
  max-width: none;
}
</style>
