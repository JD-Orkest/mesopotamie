<script setup>
/**
 * TheFooter.vue
 * Footer éditorial avec logo, tagline, liens et copyright.
 */
import { onMounted, onUnmounted, ref } from 'vue'

const contactModalOpen = ref(false)
const modalStep = ref('reasons')
const inviteForm = ref({
  place: '',
  date: '',
  time: '',
})
const formError = ref('')

function resetModalState() {
  modalStep.value = 'reasons'
  inviteForm.value = {
    place: '',
    date: '',
    time: '',
  }
  formError.value = ''
}

function openContactModal() {
  contactModalOpen.value = true
  resetModalState()
  document.body.style.overflow = 'hidden'
}

function closeContactModal() {
  contactModalOpen.value = false
  resetModalState()
  document.body.style.overflow = ''
}

function openInviteForm() {
  modalStep.value = 'form'
  formError.value = ''
}

function submitInviteForm() {
  const { place, date, time } = inviteForm.value
  if (!place.trim() || !date || !time) {
    formError.value = 'Merci de remplir le lieu, la date et l\'heure.'
    return
  }

  formError.value = ''
  modalStep.value = 'result'
}

function onKeydown(e) {
  if (e.key === 'Escape' && contactModalOpen.value) {
    closeContactModal()
  }
}

onMounted(() => {
  document.addEventListener('keydown', onKeydown)
})

onUnmounted(() => {
  document.removeEventListener('keydown', onKeydown)
  document.body.style.overflow = ''
})
</script>

<template>
  <footer class="site-footer">
    <div class="container footer-inner">

      <!-- Bloc gauche : logo + tagline -->
      <div class="footer-brand">
        <p class="footer-logo">MÉSOPOTAMIE</p>
        <p class="footer-tagline label-caps">© 2026 — Fait soif Héléna!</p>
      </div>

      <!-- Bloc droite : navigation secondaire -->
      <nav class="footer-nav" aria-label="Navigation secondaire">
        <ul>
          <li>
            <button class="label-caps footer-link footer-link-btn" @click="openContactModal">
              Contact
            </button>
          </li>
        </ul>
      </nav>

    </div>

    <!-- Ligne dorée décorative en bas -->
    <div class="footer-bottom-line" aria-hidden="true"></div>

    <!-- Modal Contact -->
    <Teleport to="body">
      <Transition name="contact-modal">
        <div
          v-if="contactModalOpen"
          class="contact-modal-backdrop"
          role="dialog"
          aria-modal="true"
          aria-label="5 raisons d'inviter Julien en date"
          @click.self="closeContactModal"
        >
          <div class="contact-modal">
            <button class="contact-modal-close" @click="closeContactModal" aria-label="Fermer">
              <span aria-hidden="true">✕</span>
            </button>

            <p class="label-caps contact-modal-label">Contact</p>
            <h3 class="contact-modal-title">5 raisons d'inviter Julien en date</h3>

            <div v-if="modalStep === 'reasons'">
              <ol class="contact-modal-list">
                <li>Il a respecté son pari (il fait des sites incroyables d'ailleurs)</li>
                <li>Il danse bien, un football de qualité</li>
                <li>Il a un côté bad boy sexy</li>
                <li>Sa version sobre est plutôt cool</li>
                <li>C'est un One Man chaud à lui tout seul, la preuve t'as souris en lisant ça</li>
              </ol>

              <div class="contact-modal-cta-wrap">
                <button class="contact-modal-cta" @click="openInviteForm">Inviter Julien</button>
              </div>
            </div>

            <form v-else-if="modalStep === 'form'" class="invite-form" @submit.prevent="submitInviteForm">
              <label class="invite-label" for="invite-place">Lieu</label>
              <input id="invite-place" v-model="inviteForm.place" class="invite-input" type="text" placeholder="Ex: Mons, Grand-Place" required />

              <div class="invite-grid">
                <div>
                  <label class="invite-label" for="invite-date">Date</label>
                  <input id="invite-date" v-model="inviteForm.date" class="invite-input" type="date" required />
                </div>
                <div>
                  <label class="invite-label" for="invite-time">Heure</label>
                  <input id="invite-time" v-model="inviteForm.time" class="invite-input" type="time" required />
                </div>
              </div>

              <p v-if="formError" class="invite-error">{{ formError }}</p>

              <div class="contact-modal-cta-wrap">
                <button class="contact-modal-cta" type="submit">Valider l'invitation</button>
              </div>
            </form>

            <div v-else class="invite-result">
              <p class="invite-result-note">
                Fais une capture d'écran du résumé et envoie là à Julien pour qu'il puisse accepter ( s'il est dans un bon mood 😜 )
              </p>

              <div class="invite-summary">
                <p><strong>Lieu:</strong> {{ inviteForm.place }}</p>
                <p><strong>Date:</strong> {{ inviteForm.date }}</p>
                <p><strong>Heure:</strong> {{ inviteForm.time }}</p>
              </div>
            </div>
          </div>
        </div>
      </Transition>
    </Teleport>
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
  color: rgba(230, 223, 211, 0.45);
  font-size: 11px;
  letter-spacing: 0.12em;
  transition: color 0.3s ease;
}

.footer-link-btn {
  background: none;
  border: none;
  padding: 0;
  cursor: pointer;
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

/* Modal contact */
.contact-modal-enter-active,
.contact-modal-leave-active {
  transition: opacity 0.28s ease;
}

.contact-modal-enter-active .contact-modal,
.contact-modal-leave-active .contact-modal {
  transition: transform 0.4s cubic-bezier(0.16, 1, 0.3, 1), opacity 0.3s ease;
}

.contact-modal-enter-from,
.contact-modal-leave-to {
  opacity: 0;
}

.contact-modal-enter-from .contact-modal {
  transform: translateY(24px) scale(0.98);
  opacity: 0;
}

.contact-modal-leave-to .contact-modal {
  transform: translateY(12px) scale(0.99);
  opacity: 0;
}

.contact-modal-backdrop {
  position: fixed;
  inset: 0;
  z-index: 1100;
  background: rgba(15, 17, 21, 0.88);
  backdrop-filter: blur(5px);
  -webkit-backdrop-filter: blur(5px);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
}

.contact-modal {
  width: min(720px, 100%);
  background:
    radial-gradient(120% 120% at 0% 0%, rgba(212, 175, 55, 0.14) 0%, rgba(212, 175, 55, 0) 45%),
    linear-gradient(135deg, #1a1d23 0%, #14161b 100%);
  border: 1px solid var(--color-sand-ghost);
  box-shadow: 0 24px 70px rgba(0, 0, 0, 0.45), 0 0 0 1px rgba(212, 175, 55, 0.12) inset;
  padding: 30px 24px 24px;
  position: relative;
  overflow: hidden;
}

.contact-modal::after {
  content: '';
  position: absolute;
  inset: auto -30% -55% auto;
  width: 420px;
  height: 240px;
  background: radial-gradient(circle, rgba(0, 79, 152, 0.18) 0%, rgba(0, 79, 152, 0) 70%);
  pointer-events: none;
}

.contact-modal-close {
  position: absolute;
  top: 12px;
  right: 12px;
  width: 36px;
  height: 36px;
  border: 1px solid var(--color-sand-ghost);
  background: rgba(15, 17, 21, 0.6);
  color: var(--color-sand);
  cursor: pointer;
  transition: transform 0.2s ease, border-color 0.2s ease, background 0.2s ease;
}

.contact-modal-close:hover {
  transform: rotate(90deg);
  border-color: var(--color-gold);
  background: rgba(212, 175, 55, 0.14);
}

.contact-modal-label {
  color: var(--color-gold);
  margin-bottom: 8px;
}

.contact-modal-title {
  font-size: clamp(22px, 4vw, 34px);
  line-height: 1.15;
  margin-bottom: 10px;
  max-width: 20ch;
}

.contact-modal-list {
  margin: 0;
  padding-left: 20px;
  display: grid;
  gap: 12px;
  color: var(--color-sand-dim);
  line-height: 1.6;
}

.contact-modal-list li {
  padding: 10px 10px 10px 2px;
  border-bottom: 1px dashed rgba(230, 223, 211, 0.12);
  transform: translateY(8px);
  opacity: 0;
  animation: rise-in 0.45s ease forwards;
}

.contact-modal-list li:nth-child(1) { animation-delay: 0.05s; }
.contact-modal-list li:nth-child(2) { animation-delay: 0.1s; }
.contact-modal-list li:nth-child(3) { animation-delay: 0.15s; }
.contact-modal-list li:nth-child(4) { animation-delay: 0.2s; }
.contact-modal-list li:nth-child(5) { animation-delay: 0.25s; }

.contact-modal-list li:last-child {
  border-bottom: none;
}

.contact-modal-cta-wrap {
  margin-top: 18px;
}

.contact-modal-cta {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  height: 42px;
  padding: 0 20px;
  border: 1px solid rgba(212, 175, 55, 0.5);
  color: var(--color-sand);
  text-decoration: none;
  letter-spacing: 0.08em;
  font-size: 12px;
  text-transform: uppercase;
  background: linear-gradient(120deg, rgba(212, 175, 55, 0.18), rgba(212, 175, 55, 0.06));
  transition: transform 0.2s ease, border-color 0.2s ease, background 0.2s ease;
  cursor: pointer;
}

.contact-modal-cta:hover {
  transform: translateY(-1px);
  border-color: var(--color-gold);
  background: linear-gradient(120deg, rgba(212, 175, 55, 0.25), rgba(212, 175, 55, 0.08));
}

.invite-form {
  display: grid;
  gap: 12px;
}

.invite-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 12px;
}

.invite-label {
  display: block;
  font-size: 11px;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--color-gold);
  margin-bottom: 6px;
}

.invite-input {
  width: 100%;
  height: 42px;
  border: 1px solid rgba(230, 223, 211, 0.2);
  background: rgba(12, 13, 17, 0.6);
  color: var(--color-sand);
  padding: 0 12px;
}

.invite-input:focus {
  outline: none;
  border-color: rgba(212, 175, 55, 0.5);
}

.invite-error {
  color: #ffb4b4;
  font-size: 13px;
  margin: 2px 0 0;
}

.invite-result {
  margin-top: 10px;
  text-align: center;
  padding: 18px 10px 8px;
}

.invite-result-note {
  margin: 0 auto 12px;
  max-width: 44ch;
  color: var(--color-sand);
  font-family: var(--font-display);
  font-size: clamp(20px, 3vw, 30px);
  line-height: 1.6;
}

.invite-summary {
  max-width: 460px;
  margin: 0 auto;
  padding: 14px 16px;
  text-align: left;
  border: 1px dashed rgba(230, 223, 211, 0.25);
  background: rgba(12, 13, 17, 0.5);
}

.invite-summary p {
  margin: 0;
  color: rgba(230, 223, 211, 0.82);
  line-height: 1.7;
}

.invite-summary p + p {
  margin-top: 4px;
}

@keyframes rise-in {
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

@media (max-width: 560px) {
  .contact-modal {
    padding: 24px 18px 20px;
  }

  .invite-grid {
    grid-template-columns: 1fr;
  }
}
</style>
