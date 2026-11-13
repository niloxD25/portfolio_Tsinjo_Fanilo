
<script setup>
import { ref } from 'vue'

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
    icon: 'https://api.iconify.design/logos/github-icon.svg'
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
    note: 'Les champs marqués sont obligatoires.',
    required: 'Obligatoire'
  },

  en: {
    eyebrow: 'CONTACT',
    title: 'Let’s build something together.',
    introduction:
      'Have a project, a professional opportunity or simply want to connect? I would be happy to hear from you.',
    emailLabel: 'EMAIL',
    locationLabel: 'LOCATION',
    location: 'Antananarivo, Madagascar',
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
    note: 'Fields marked as required must be completed.',
    required: 'Required'
  }
}

function sendMessage() {
  const subject = encodeURIComponent(form.value.subject)
  const body = encodeURIComponent(
    `Nom : ${form.value.name}\n` +
    `Email : ${form.value.email}\n\n` +
    `Message :\n${form.value.message}`
  )

  window.location.href =
    `mailto:${contactEmail}?subject=${subject}&body=${body}`
}
</script>

<template>
  <section id="contact" class="contact-section">
    <div class="contact-container">

      <!-- HEADER -->
      <div class="contact-header">
        <span class="section-label">
          <span class="label-line"></span>
          {{ content[lang].eyebrow }}
        </span>

        <h2>{{ content[lang].title }}</h2>

        <p>{{ content[lang].introduction }}</p>
      </div>

      <!-- CONTACT CONTENT -->
      <div class="contact-grid">

        <!-- LEFT COLUMN -->
        <div class="contact-details">

          <div class="contact-item">
            <span class="contact-label">
              {{ content[lang].emailLabel }}
            </span>

            <a :href="`mailto:${contactEmail}`">
              {{ contactEmail }}
            </a>
          </div>

          <div class="contact-item">
            <span class="contact-label">
              {{ content[lang].locationLabel }}
            </span>

            <p>{{ content[lang].location }}</p>
          </div>

          
            <div class="contact-socials">
            <span class="contact-label">
                {{ content[lang].socialLabel }}
            </span>

            <div class="social-links">
                <a
                v-for="contact in contacts"
                :key="contact.name"
                :href="contact.url"
                :aria-label="contact.name"
                :title="contact.name"
                target="_blank"
                rel="noopener noreferrer"
                >
                <img
                    :src="contact.icon"
                    :alt="contact.name"
                    loading="lazy"
                />
                </a>
            </div>
            </div>


          <div class="contact-decoration">
            <span>LET'S</span>
            <span>CONNECT.</span>
          </div>

        </div>

        <!-- RIGHT COLUMN -->
        <div class="contact-form-container">

          <h3>{{ content[lang].formTitle }}</h3>

          <form @submit.prevent="sendMessage">

            <div class="form-row">
              <div class="form-group">
                <label for="contact-name">
                  {{ content[lang].name }}
                </label>

                <input
                  id="contact-name"
                  v-model="form.name"
                  type="text"
                  :placeholder="content[lang].namePlaceholder"
                  required
                />
              </div>

              <div class="form-group">
                <label for="contact-email">
                  {{ content[lang].email }}
                </label>

                <input
                  id="contact-email"
                  v-model="form.email"
                  type="email"
                  :placeholder="content[lang].emailPlaceholder"
                  required
                />
              </div>
            </div>

            <div class="form-group">
              <label for="contact-subject">
                {{ content[lang].subject }}
              </label>

              <input
                id="contact-subject"
                v-model="form.subject"
                type="text"
                :placeholder="content[lang].subjectPlaceholder"
                required
              />
            </div>

            <div class="form-group">
              <label for="contact-message">
                {{ content[lang].message }}
              </label>

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
                <span>↗</span>
              </button>
            </div>

          </form>
        </div>

      </div>
    </div>
  </section>
</template>

<style scoped>
.contact-section {
  background: #111;
  color: #fff;
  padding: 120px 7%;
}

.contact-container {
  max-width: 1400px;
  margin: 0 auto;
}

.section-label {
  display: inline-flex;
  align-items: center;
  gap: 12px;
  color: var(--color-accent);
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 2px;
}

.label-line {
  width: 30px;
  height: 1px;
  background: var(--color-accent);
}

.contact-header {
  max-width: 800px;
  margin-bottom: 65px;
}

.contact-header h2 {
  margin-top: 30px;
  font-size: clamp(38px, 5vw, 68px);
  line-height: 1.1;
  letter-spacing: -2px;
  font-weight: 600;
}

.contact-header > p {
  max-width: 600px;
  margin-top: 22px;
  color: #999;
  font-size: 14px;
  line-height: 1.8;
}

.contact-grid {
  display: grid;
  grid-template-columns: 0.8fr 1.2fr;
  gap: 70px;
}

.contact-details {
  display: flex;
  flex-direction: column;
  gap: 35px;
}

.contact-item,
.contact-socials {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.contact-label {
  color: #777;
  font-size: 10px;
  font-weight: 600;
  letter-spacing: 2px;
}

.contact-item a,
.contact-item p {
  color: #fff;
  font-size: 15px;
  text-decoration: none;
}

.contact-item a {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  width: fit-content;
  transition: color 0.3s;
}

.contact-item a span,
.social-links a span {
  color: var(--color-accent);
}

.contact-item a:hover {
  color: var(--color-accent);
}


.social-links {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  gap: 18px;
}

.social-links a {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 46px;
  height: 46px;
  background: #202020;
  border: 1px solid #383838;
  transition: all 0.3s ease;
}

.social-links a img {
  width: 21px;
  height: 21px;
  object-fit: contain;
  transition: transform 0.3s ease;
}

.social-links a:hover {
  border-color: var(--color-accent);
  transform: translateY(-4px);
}

.social-links a:hover img {
  transform: scale(1.1);
}

.contact-decoration {
  display: flex;
  flex-direction: column;
  margin-top: auto;
  padding-top: 50px;
  color: #292929;
  font-size: clamp(35px, 5vw, 65px);
  font-weight: 700;
  line-height: 0.95;
  letter-spacing: -2px;
}

.contact-decoration span:last-child {
  color: var(--color-accent);
}

.contact-form-container {
  padding: 35px;
}

.contact-form-container h3 {
  margin-bottom: 35px;
  font-size: 22px;
  font-weight: 600;
}

.form-row {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 20px;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 25px;
}

.form-group label {
  color: #ccc;
  font-size: 12px;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 14px 15px;
  background: #222;
  border: 1px solid #383838;
  outline: none;
  color: #fff;
  font-family: inherit;
  font-size: 13px;
  transition: border-color 0.3s;
}

.form-group input:focus,
.form-group textarea:focus {
  border-color: var(--color-accent);
}

.form-group input::placeholder,
.form-group textarea::placeholder {
  color: #666;
}

.form-group textarea {
  resize: vertical;
  min-height: 130px;
}

.form-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 20px;
}

.form-footer p {
  color: #777;
  font-size: 11px;
}

.contact-button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
  padding: 15px 22px;
  background: var(--color-accent);
  border: 1px solid var(--color-accent);
  color: #171717;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 1px;
  cursor: pointer;
  transition: all 0.3s;
}

.contact-button:hover {
  background: transparent;
  color: var(--color-accent);
}

/* Tablet */
@media (max-width: 900px) {
  .contact-section {
    padding: 90px 6%;
  }

  .contact-grid {
    grid-template-columns: 1fr;
    gap: 50px;
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
    letter-spacing: -1px;
  }

  .contact-form-container {
    padding: 22px;
  }

  .form-row {
    grid-template-columns: 1fr;
    gap: 0;
  }

  .form-footer {
    align-items: flex-start;
    flex-direction: column;
  }

  .contact-button {
    width: 100%;
  }
}
</style>
