<script setup>
import { ref, onBeforeUnmount, onMounted } from 'vue'

defineProps({
  lang: {
    type: String,
    default: 'fr'
  }
})

const form = ref({
  name: '',
  email: '',
  subject: '',
  message: ''
})

const contactEmail = 'fanilotsinjo@gmail.com'

const contacts = [
  {
    name: 'Facebook',
    url: 'https://www.facebook.com/fanilotsinjo.andriamanalintsoa',
    icon: 'https://api.iconify.design/logos/facebook.svg'
  },
  {
    name: 'LinkedIn',
    url: 'https://www.linkedin.com/in/tsinjo-fanilo-andriamanalintsoa-1102b4440/',
    icon: 'https://api.iconify.design/logos/linkedin-icon.svg'
  },
  {
    name: 'GitHub',
    url: 'https://github.com/niloxD25',
    icon: 'https://api.iconify.design/logos/github-icon.svg',
    invert: true
  },
  {
    name: 'WhatsApp',
    url: 'https://wa.me/261349947698',
    icon: 'https://api.iconify.design/logos/whatsapp-icon.svg'
  }
]

const content = {
  fr: {
    eyebrow: 'CONTACT',
    title: 'Construisons quelque chose ensemble.',
    introduction:
      'Vous avez un projet, une opportunité professionnelle ou simplement envie d’échanger ? Je serais ravi de discuter avec vous.',
    emailLabel: 'EMAIL',
    locationLabel: 'LOCALISATION',
    location: 'Antananarivo, Madagascar',
    copy: 'Copier',
    copied: 'Copié !',
    socialLabel: 'RETROUVEZ-MOI AUSSI SUR',
    formTitle: 'Envoyez-moi un message',
    name: 'Votre nom',
    email: 'Votre adresse email',
    subject: 'Sujet',
    message: 'Votre message',
    namePlaceholder: 'Entrez votre nom',
    emailPlaceholder: 'exemple@email.com',
    subjectPlaceholder: 'Objet de votre message',
    messagePlaceholder: 'Parlez-moi de votre projet...',
    button: 'ENVOYER LE MESSAGE',
    note: 'Tous les champs sont obligatoires.',
    sent: 'Votre messagerie s’ouvre : il ne reste qu’à envoyer le message.',
    decoration: ['ÉCHANGEONS', 'ENSEMBLE.']
  },

  en: {
    eyebrow: 'CONTACT',
    title: 'Let’s build something together.',
    introduction:
      'Have a project, a professional opportunity or simply want to connect? I would be happy to hear from you.',
    emailLabel: 'EMAIL',
    locationLabel: 'LOCATION',
    location: 'Antananarivo, Madagascar',
    copy: 'Copy',
    copied: 'Copied!',
    socialLabel: 'ALSO FIND ME ON',
    formTitle: 'Send me a message',
    name: 'Your name',
    email: 'Your email address',
    subject: 'Subject',
    message: 'Your message',
    namePlaceholder: 'Enter your name',
    emailPlaceholder: 'example@email.com',
    subjectPlaceholder: 'Message subject',
    messagePlaceholder: 'Tell me about your project...',
    button: 'SEND MESSAGE',
    note: 'All fields are required.',
    sent: 'Your mail app is opening: just hit send to deliver the message.',
    decoration: ['LET’S', 'CONNECT.']
  }
}

/* ---------- Copier l'email ---------- */
const copied = ref(false)
let copyTimer = null

async function copyEmail() {
  try {
    await navigator.clipboard.writeText(contactEmail)
    copied.value = true
    clearTimeout(copyTimer)
    copyTimer = setTimeout(() => (copied.value = false), 2000)
  } catch {
    window.location.href = `mailto:${contactEmail}`
  }
}

/* ---------- Envoi (ouvre le client mail) ---------- */
const sent = ref(false)
let sentTimer = null

function sendMessage() {
  const subject = encodeURIComponent(form.value.subject)
  const body = encodeURIComponent(
    `Nom : ${form.value.name}\n` +
    `Email : ${form.value.email}\n\n` +
    `Message :\n${form.value.message}`
  )

  sent.value = true
  clearTimeout(sentTimer)
  sentTimer = setTimeout(() => (sent.value = false), 8000)

  window.location.href =
    `mailto:${contactEmail}?subject=${subject}&body=${body}`
}

const root = ref(null)
let observer = null

onMounted(() => {
  const items = root.value?.querySelectorAll('.reveal') ?? []

  if (!('IntersectionObserver' in window)) {
    items.forEach((el) => el.classList.add('visible'))
    return
  }

  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('visible')
          observer.unobserve(entry.target)
        }
      })
    },
    { threshold: 0.12 }
  )

  items.forEach((el) => observer.observe(el))
})

onBeforeUnmount(() => {
  observer?.disconnect()
  clearTimeout(copyTimer)
  clearTimeout(sentTimer)
})
</script>

<template>
  <section id="contact" ref="root" class="contact-section">
    <div class="contact-container">

      <div class="contact-header">
        <span class="section-label reveal">
          {{ content[lang].eyebrow }}
        </span>

        <h2 class="reveal" style="--d: 0.08s">{{ content[lang].title }}</h2>

        <p class="reveal" style="--d: 0.16s">{{ content[lang].introduction }}</p>
      </div>

      <div class="contact-grid">

        <div class="contact-details">

          <div class="info-card reveal">
            <span class="info-icon" aria-hidden="true">
              <svg viewBox="0 0 24 24" width="20" height="20" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
                <rect x="3" y="5" width="18" height="14" rx="3" />
                <path d="m4 7 8 6 8-6" />
              </svg>
            </span>

            <div class="info-text">
              <span class="contact-label">{{ content[lang].emailLabel }}</span>
              <a :href="`mailto:${contactEmail}`">{{ contactEmail }}</a>
            </div>

            <button type="button" class="copy-btn" @click="copyEmail">
              <span aria-live="polite">
                {{ copied ? content[lang].copied : content[lang].copy }}
              </span>
            </button>
          </div>

          <div class="info-card reveal" style="--d: 0.08s">
            <span class="info-icon" aria-hidden="true">
              <svg viewBox="0 0 24 24" width="20" height="20" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
                <path d="M12 21s7-5.6 7-11a7 7 0 1 0-14 0c0 5.4 7 11 7 11Z" />
                <circle cx="12" cy="10" r="2.5" />
              </svg>
            </span>

            <div class="info-text">
              <span class="contact-label">{{ content[lang].locationLabel }}</span>
              <p>{{ content[lang].location }}</p>
            </div>
          </div>

          <div class="contact-socials reveal" style="--d: 0.16s">
            <span class="contact-label">{{ content[lang].socialLabel }}</span>

            <div class="social-links">
              <a
                v-for="contact in contacts"
                :key="contact.name"
                :href="contact.url"
                target="_blank"
                rel="noopener noreferrer"
              >
                <img
                  :src="contact.icon"
                  alt=""
                  width="18"
                  height="18"
                  loading="lazy"
                  :class="{ invert: contact.invert }"
                />
                {{ contact.name }}
              </a>
            </div>
          </div>

          <div class="contact-decoration" aria-hidden="true">
            <span>{{ content[lang].decoration[0] }}</span>
            <span>{{ content[lang].decoration[1] }}</span>
          </div>

        </div>

        <div class="contact-form-container reveal" style="--d: 0.12s">

          <h3>{{ content[lang].formTitle }}</h3>

          <form @submit.prevent="sendMessage">

            <div class="form-row">
              <div class="form-group">
                <label for="contact-name">{{ content[lang].name }}</label>
                <input
                  id="contact-name"
                  v-model="form.name"
                  type="text"
                  autocomplete="name"
                  :placeholder="content[lang].namePlaceholder"
                  required
                />
              </div>

              <div class="form-group">
                <label for="contact-email">{{ content[lang].email }}</label>
                <input
                  id="contact-email"
                  v-model="form.email"
                  type="email"
                  autocomplete="email"
                  :placeholder="content[lang].emailPlaceholder"
                  required
                />
              </div>
            </div>

            <div class="form-group">
              <label for="contact-subject">{{ content[lang].subject }}</label>
              <input
                id="contact-subject"
                v-model="form.subject"
                type="text"
                :placeholder="content[lang].subjectPlaceholder"
                required
              />
            </div>

            <div class="form-group form-group-message">
              <label for="contact-message">{{ content[lang].message }}</label>
              <textarea
                id="contact-message"
                v-model="form.message"
                rows="5"
                :placeholder="content[lang].messagePlaceholder"
                required
              ></textarea>
            </div>

            <div class="form-footer">
              <p>{{ content[lang].note }}</p>

              <button type="submit" class="contact-button">
                {{ content[lang].button }}
                <span class="arrow" aria-hidden="true">↗</span>
              </button>
            </div>

            <p v-if="sent" class="form-status" role="status">
              {{ content[lang].sent }}
            </p>

          </form>
        </div>

      </div>
    </div>
  </section>
</template>

<style scoped>
/* Même modèle de boîte pour tous les éléments de la section */
.contact-section *,
.contact-section *::before,
.contact-section *::after {
  box-sizing: border-box;
}

.contact-section {
  --accent: var(--color-accent, #e8a45c);
  position: relative;
  overflow: hidden;
  background: #111;
  color: #fff;
  padding: 120px 7%;
}

.contact-container {
  position: relative;
  max-width: 1400px;
  margin: 0 auto;
}

/* Apparition au scroll */
.reveal {
  opacity: 0;
}

.reveal.visible {
  opacity: 1;
  animation: rise 0.7s cubic-bezier(0.2, 0.7, 0.2, 1) var(--d, 0s) backwards;
}

@keyframes rise {
  from {
    opacity: 0;
    transform: translateY(22px);
  }
  to {
    opacity: 1;
    transform: none;
  }
}

/* Label */
.section-label {
  display: inline-flex;
  align-items: center;
  gap: 12px;
  color: var(--accent);
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 2.5px;
}

/* En-tête */
.contact-header {
  max-width: 800px;
  margin-bottom: 60px;
}

.contact-header h2 {
  margin-top: 28px;
  font-size: clamp(38px, 5vw, 68px);
  line-height: 1.08;
  font-weight: 700;
  letter-spacing: -0.035em;
  background-clip: text;
  color: #fff; /* repli */
}

.contact-header > p {
  max-width: 600px;
  margin-top: 22px;
  color: #a0a0a0;
  font-size: 14.5px;
  line-height: 1.8;
}

/* Grille */
.contact-grid {
  display: grid;
  grid-template-columns: 0.8fr 1.2fr;
  gap: clamp(40px, 6vw, 80px);
  align-items: stretch;
}

.contact-details {
  display: flex;
  flex-direction: column;
  gap: 14px;
}

.contact-label {
  color: #7a7a7a;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 2px;
}

/* Cartes d'information */
.info-card {
  display: flex;
  align-items: center;
  gap: 16px;
  padding: 18px 20px;
  border-radius: 18px;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.08);
  transition: border-color 0.3s, background 0.3s;
}

.info-card:hover {
  border-color: rgba(232, 164, 92, 0.35);
  background: rgba(232, 164, 92, 0.04);
}

.info-icon {
  display: grid;
  place-items: center;
  width: 44px;
  height: 44px;
  flex-shrink: 0;
  border-radius: 12px;
  background: rgba(232, 164, 92, 0.12);
  border: 1px solid rgba(232, 164, 92, 0.25);
  color: var(--accent);
}

.info-text {
  display: flex;
  flex-direction: column;
  gap: 6px;
  min-width: 0;
  flex: 1;
}

.info-text a,
.info-text p {
  color: #fff;
  font-size: 15px;
  text-decoration: none;
  overflow-wrap: anywhere;
}

.info-text a {
  width: fit-content;
  transition: color 0.3s;
}

.info-text a:hover {
  color: var(--accent);
}

.copy-btn {
  flex-shrink: 0;
  padding: 8px 14px;
  border-radius: 999px;
  border: 1px solid rgba(255, 255, 255, 0.15);
  background: transparent;
  color: #ccc;
  font-family: inherit;
  font-size: 11px;
  font-weight: 600;
  cursor: pointer;
  transition: color 0.25s, border-color 0.25s, background 0.25s;
}

.copy-btn:hover {
  color: #111;
  background: var(--accent);
  border-color: var(--accent);
}

/* Réseaux sociaux */
.contact-socials {
  display: flex;
  flex-direction: column;
  gap: 14px;
  margin-top: 18px;
}

.social-links {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.social-links a {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding: 10px 16px 10px 12px;
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.1);
  color: #d0d0d0;
  font-size: 12px;
  font-weight: 500;
  text-decoration: none;
  transition: transform 0.25s, border-color 0.25s, background 0.25s,
    color 0.25s;
}

.social-links a img {
  width: 18px;
  height: 18px;
  object-fit: contain;
}

.social-links a img.invert {
  filter: invert(1);
}

.social-links a:hover {
  transform: translateY(-3px);
  color: #fff;
  border-color: rgba(232, 164, 92, 0.5);
  background: rgba(232, 164, 92, 0.08);
}

/* Décoration */
.contact-decoration {
  display: flex;
  flex-direction: column;
  margin-top: auto;
  padding-top: 40px;
  font-size: clamp(35px, 5vw, 65px);
  font-weight: 800;
  line-height: 0.95;
  letter-spacing: -0.04em;
  user-select: none;
}

.contact-decoration span:first-child {
  color: transparent;
  -webkit-text-stroke: 1.5px rgba(255, 255, 255, 0.12);
}

.contact-decoration span:last-child {
  color: var(--accent);
}

/* Formulaire : la hauteur de la carte suit la colonne de gauche */
.contact-form-container {
  display: flex;
  flex-direction: column;
  padding: clamp(24px, 3.5vw, 42px);
  border-radius: 26px;
  background: linear-gradient(
    145deg,
    rgba(255, 255, 255, 0.055),
    rgba(255, 255, 255, 0.015)
  );
  border: 1px solid rgba(255, 255, 255, 0.09);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
}

.contact-form-container h3 {
  margin-bottom: 30px;
  font-size: 22px;
  font-weight: 600;
  letter-spacing: -0.01em;
}

.contact-form-container form {
  display: flex;
  flex-direction: column;
  flex: 1;
}

/* Champs */
.form-row {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 0 20px;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 9px;
  min-width: 0;
  margin-bottom: 20px;
}

.form-group-message {
  flex: 1;
}

.form-group label {
  color: #bdbdbd;
  font-size: 12px;
  font-weight: 500;
}

.form-group input,
.form-group textarea {
  display: block;
  width: 100%;
  min-height: 50px;
  padding: 14px 16px;
  border-radius: 14px;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.1);
  outline: none;
  color: #fff;
  font-family: inherit;
  font-size: 14px;
  line-height: 1.4;
  -webkit-appearance: none;
  appearance: none;
  transition: border-color 0.25s, box-shadow 0.25s, background 0.25s;
}

.form-group input:focus,
.form-group textarea:focus {
  border-color: var(--accent);
  background: rgba(255, 255, 255, 0.06);
  box-shadow: 0 0 0 4px rgba(232, 164, 92, 0.14);
}

.form-group input::placeholder,
.form-group textarea::placeholder {
  color: #666;
}

.form-group textarea {
  flex: 1;
  min-height: 140px;
  resize: vertical;
}

/* Remplissage automatique du navigateur (évite le fond blanc/jaune) */
.form-group input:-webkit-autofill {
  -webkit-text-fill-color: #fff;
  caret-color: #fff;
  box-shadow: 0 0 0 1000px #1c1c1c inset;
}

.form-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 20px;
}

.form-footer p {
  color: #7a7a7a;
  font-size: 11px;
}

.contact-button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 16px;
  padding: 8px 8px 8px 24px;
  border: none;
  border-radius: 999px;
  background: var(--accent);
  color: #171717;
  font-family: inherit;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 1px;
  cursor: pointer;
  transition: transform 0.25s, box-shadow 0.25s;
}

.contact-button .arrow {
  display: grid;
  place-items: center;
  width: 34px;
  height: 34px;
  border-radius: 50%;
  background: #171717;
  color: var(--accent);
  font-size: 15px;
  transition: transform 0.25s;
}

.contact-button:hover {
  transform: translateY(-2px);
}

.contact-button:hover .arrow {
  transform: translate(2px, -2px);
}

.form-status {
  margin-top: 18px;
  padding: 12px 16px;
  border-radius: 12px;
  background: rgba(74, 222, 128, 0.08);
  border: 1px solid rgba(74, 222, 128, 0.25);
  color: #86efac;
  font-size: 12px;
  line-height: 1.6;
}

/* Focus clavier */
.contact-button:focus-visible,
.copy-btn:focus-visible,
.social-links a:focus-visible,
.info-text a:focus-visible {
  outline: 2px solid var(--accent);
  outline-offset: 3px;
}

/* Tablette */
@media (max-width: 900px) {
  .contact-section {
    padding: 90px 6%;
  }

  .contact-grid {
    grid-template-columns: 1fr;
    gap: 45px;
  }

  .contact-decoration {
    display: none;
  }
}

/* Mobile */
@media (max-width: 600px) {
  .contact-section {
    padding: 75px 6%;
  }

  .contact-header {
    margin-bottom: 40px;
  }

  .contact-header h2 {
    font-size: 40px;
  }

  .info-card {
    padding: 16px;
    gap: 12px;
  }

  .form-row {
    grid-template-columns: 1fr;
    gap: 0;
  }

  .form-footer {
    align-items: stretch;
    flex-direction: column;
  }

  .contact-button {
    justify-content: space-between;
    width: 100%;
  }
}

@media (prefers-reduced-motion: reduce) {
  .reveal,
  .reveal.visible {
    opacity: 1;
    animation: none;
  }

  * {
    transition: none !important;
  }
}
</style>