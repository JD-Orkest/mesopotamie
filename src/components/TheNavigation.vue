<script setup>
/**
 * TheNavigation.vue
 * Barre de navigation fixe avec backdrop-blur, disparaît au scroll bas.
 */
import { ref } from 'vue'

defineProps({
  visible: {
    type: Boolean,
    default: true,
  },
})

const menuOpen = ref(false)

function scrollTo(id) {
  menuOpen.value = false
  const el = document.getElementById(id)
  if (el) el.scrollIntoView({ behavior: 'smooth' })
}

const navItems = [
  { label: 'Époques',       id: 'epoques'      },
  { label: 'Chaoskampf',    id: 'chaoskampf'   },
  { label: 'Transmission',  id: 'transmission' },
  { label: 'Rituels',       id: 'rituels'      },
]
</script>

<template>
  <header :class="['site-nav', { 'site-nav--hidden': !visible }]">
    <nav class="container nav-inner">
      <!-- Logo -->
      <button class="nav-logo label-caps" @click="scrollTo('hero')">
        Mésopotamie
      </button>

      <!-- Liens desktop -->
      <ul class="nav-links">
        <li v-for="item in navItems" :key="item.id">
          <button class="nav-link label-caps" @click="scrollTo(item.id)">
            {{ item.label }}
          </button>
        </li>
      </ul>

      <!-- CTA desktop -->
      <button class="btn nav-cta" @click="scrollTo('epoques')">
        Explorer
      </button>

      <!-- Bouton hamburger mobile -->
      <button
        class="nav-hamburger"
        :class="{ 'is-open': menuOpen }"
        aria-label="Menu"
        @click="menuOpen = !menuOpen"
      >
        <span></span><span></span>
      </button>
    </nav>

    <!-- Menu mobile -->
    <div :class="['nav-mobile-menu', { 'is-open': menuOpen }]">
      <ul>
        <li v-for="item in navItems" :key="item.id">
          <button class="nav-link label-caps" @click="scrollTo(item.id)">
            {{ item.label }}
          </button>
        </li>
        <li>
          <button class="btn" @click="scrollTo('epoques')">Explorer</button>
        </li>
      </ul>
    </div>
  </header>
</template>

<style scoped>
.site-nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  background-color: rgba(15, 17, 21, 0.75);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(230, 223, 211, 0.08);
  transform: translateY(0);
  transition: transform 0.4s var(--ease-out);
}

.site-nav--hidden {
  transform: translateY(-100%);
}

.nav-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 64px;
}

.nav-logo {
  background: none;
  border: none;
  cursor: pointer;
  color: var(--color-sand);
  letter-spacing: 0.2em;
  font-size: 13px;
}

.nav-links {
  display: none;
  list-style: none;
  gap: 40px;
}

@media (min-width: 1024px) {
  .nav-links {
    display: flex;
  }
}

.nav-link {
  background: none;
  border: none;
  cursor: pointer;
  color: var(--color-sand-dim);
  transition: color 0.3s ease;
  padding: 4px 0;
  position: relative;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: -2px;
  left: 0;
  width: 0;
  height: 1px;
  background-color: var(--color-gold);
  transition: width 0.3s var(--ease-out);
}

.nav-link:hover {
  color: var(--color-sand);
}

.nav-link:hover::after {
  width: 100%;
}

.nav-cta {
  display: none;
  padding: 10px 20px;
  font-size: 11px;
}

@media (min-width: 1024px) {
  .nav-cta {
    display: inline-flex;
  }
}

/* ── Hamburger ── */
.nav-hamburger {
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 6px;
  width: 32px;
  height: 32px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 4px;
}

@media (min-width: 1024px) {
  .nav-hamburger {
    display: none;
  }
}

.nav-hamburger span {
  display: block;
  width: 100%;
  height: 1px;
  background-color: var(--color-sand);
  transition: transform 0.3s ease, opacity 0.3s ease;
}

.nav-hamburger.is-open span:first-child {
  transform: translateY(7px) rotate(45deg);
}

.nav-hamburger.is-open span:last-child {
  transform: translateY(-7px) rotate(-45deg);
}

/* ── Menu mobile ── */
.nav-mobile-menu {
  max-height: 0;
  overflow: hidden;
  background-color: rgba(15, 17, 21, 0.95);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  transition: max-height 0.5s var(--ease-out);
}

.nav-mobile-menu.is-open {
  max-height: 400px;
}

.nav-mobile-menu ul {
  list-style: none;
  padding: 24px var(--margin-mobile) 32px;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.nav-mobile-menu .nav-link {
  font-size: 14px;
}

@media (min-width: 1024px) {
  .nav-mobile-menu {
    display: none;
  }
}
</style>
