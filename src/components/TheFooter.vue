<script setup>
/**
 * TheFooter.vue
 * Footer éditorial avec logo, tagline, liens et copyright.
 */
</script>

<template>
  <footer class="site-footer">
    <div class="container footer-inner">

      <!-- Bloc gauche : logo + tagline -->
      <div class="footer-brand">
        <p class="footer-logo">MÉSOPOTAMIE</p>
        <p class="footer-tagline label-caps">© 2026 — Si tu vois ça, hele.smk te doit un verre.</p>
      </div>

      <!-- Bloc droite : navigation secondaire -->
      <nav class="footer-nav" aria-label="Navigation secondaire">
        <ul>
          <li><a href="#" class="label-caps footer-link">Archives</a></li>
          <li><a href="#" class="label-caps footer-link">Méthodologie</a></li>
          <li><a href="#" class="label-caps footer-link">Mentions légales</a></li>
          <li><a href="#" class="label-caps footer-link">Contact</a></li>
        </ul>
      </nav>

    </div>

    <!-- Ligne dorée décorative en bas -->
    <div class="footer-bottom-line" aria-hidden="true"></div>
  </footer>
</template>

<style scoped>
.site-footer {
  background-color: var(--color-surface);
  border-top: 1px solid var(--color-sand-ghost);
  padding: 64px 0 0;
  position: relative;
}

.footer-inner {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 40px;
  padding-bottom: 64px;
}

@media (max-width: 640px) {
  .footer-inner {
    flex-direction: column;
    gap: 48px;
  }
}

/* ── Marque ── */
.footer-logo {
  font-family: var(--font-display);
  font-size: clamp(28px, 5vw, 48px);
  font-weight: 700;
  letter-spacing: -0.03em;
  color: var(--color-sand);
  max-width: none;
  line-height: 1;
  margin-bottom: 16px;
}

.footer-tagline {
  color: rgba(230, 223, 211, 0.35);
  line-height: 1.7;
  max-width: none;
}

/* ── Navigation secondaire ── */
.footer-nav ul {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 16px;
  text-align: right;
}

@media (max-width: 640px) {
  .footer-nav ul {
    flex-direction: row;
    flex-wrap: wrap;
    text-align: left;
    gap: 20px 32px;
  }
}

.footer-link {
  text-decoration: none;
  color: rgba(230, 223, 211, 0.45);
  font-size: 11px;
  letter-spacing: 0.12em;
  transition: color 0.3s ease;
}

.footer-link:hover {
  color: var(--color-sand);
}

/* Ligne dorée au bas absolu */
.footer-bottom-line {
  height: 2px;
  background: linear-gradient(
    to right,
    transparent,
    var(--color-gold) 30%,
    var(--color-gold) 70%,
    transparent
  );
  opacity: 0.4;
}
</style>
