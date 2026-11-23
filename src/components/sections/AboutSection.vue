<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

defineProps({
  lang: {
    type: String,
    default: 'fr'
  }
})

const content = {
  fr: {
    eyebrow: 'À PROPOS DE MOI',
    title: 'Créer des solutions, transformer des idées.',
    introduction: 'Je suis développeur Full-stack basé à Antananarivo, Madagascar.',
    paragraphs: [
      'Titulaire d’une Licence en informatique à ITUniversity, je m’intéresse particulièrement à la conception et au développement d’applications web et de solutions numériques.',
      'Mon parcours m’a permis de travailler sur des projets concrets associant développement logiciel, gestion de données et outils de collecte sur le terrain. J’ai notamment participé à des activités de développement et de collecte de données dans les domaines du développement local et de l’Eau, de l’Assainissement et de l’Hygiène (EAH).',
      'J’accorde une importance particulière à la qualité du code, à l’expérience utilisateur et à la création de solutions utiles, évolutives et faciles à maintenir.'
    ],
    focusTitle: 'MES DOMAINES',
    areas: [
      {
        number: '01',
        title: 'Développement Web',
        description: 'Conception d’applications web modernes et d’interfaces intuitives.'
      },
      {
        number: '02',
        title: 'Développement Applicatif',
        description: 'Création de solutions métier adaptées aux besoins des utilisateurs.'
      },
      {
        number: '03',
        title: 'Gestion de données',
        description: 'Collecte, structuration, traitement et exploitation des données.'
      }
    ],
    educations: [
      {
        degree: 'Licence en informatique',
        institution: 'ITUniversity',
        url: 'https://www.ituniversity.mg/',
        location: 'Antananarivo, Madagascar',
        period: '',
        description: ''
      }
    ],
    educationTitle: 'FORMATION',
    button: 'Télécharger mon CV'
  },

  en: {
    eyebrow: 'ABOUT ME',
    title: 'Building solutions, turning ideas into reality.',
    introduction: 'I am a Full-stack Developer based in Antananarivo, Madagascar.',
    paragraphs: [
      'Holding a Bachelor’s degree in Computer Science from ITUniversity, I am particularly interested in designing and developing web applications and digital solutions.',
      'My experience includes practical projects combining software development, data management and field data collection tools. I have contributed to development and data collection activities in local development and Water, Sanitation and Hygiene (WASH) projects.',
      'I place particular importance on code quality, user experience and building useful, scalable and maintainable solutions.'
    ],
    focusTitle: 'MY AREAS OF FOCUS',
    areas: [
      {
        number: '01',
        title: 'Web Development',
        description: 'Building modern web applications and intuitive interfaces.'
      },
      {
        number: '02',
        title: 'Application Development',
        description: 'Creating business solutions tailored to user needs.'
      },
      {
        number: '03',
        title: 'Data Management',
        description: 'Data collection, structuring, processing and analysis.'
      }
    ],
    educations: [
      {
        degree: 'Bachelor’s Degree in Computer Science',
        institution: 'ITUniversity',
        url: 'https://www.ituniversity.mg/',
        location: 'Antananarivo, Madagascar',
        period: '',
        description: ''
      }
    ],
    educationTitle: 'EDUCATION',
    button: 'Download my resume'
  }
}

// Apparition progressive au scroll
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
    { threshold: 0.15 }
  )

  items.forEach((el) => observer.observe(el))
})

onBeforeUnmount(() => observer?.disconnect())
</script>

<template>
  <section id="about" ref="root" class="about-section">
    <div class="about-container">

      <!-- COLONNE GAUCHE -->
      <div class="about-intro">

        <span class="section-label reveal">
          {{ content[lang].eyebrow }}
        </span>

        <h2 class="reveal" style="--d: 0.08s">
          {{ content[lang].title }}
        </h2>

        <h3 class="reveal" style="--d: 0.16s">
          {{ content[lang].introduction }}
        </h3>

        <div class="about-description">
          <p
            v-for="(paragraph, i) in content[lang].paragraphs"
            :key="i"
            class="reveal"
            :style="{ '--d': `${0.24 + i * 0.08}s` }"
          >
            {{ paragraph }}
          </p>
        </div>

        <a
          href="/portfolio_Tsinjo_Fanilo/documents/CV_ANDRIAMANALINTSOA_Tsinjo_Fanilo_WR.pdf"
          download="CV_ANDRIAMANALINTSOA_Tsinjo_Fanilo_WR.pdf"
          class="about-button reveal"
          style="--d: 0.5s"
        >
          {{ content[lang].button }}
          <span class="arrow" aria-hidden="true">↓</span>
        </a>

      </div>

      <!-- COLONNE DROITE -->
      <div class="about-details">

        <div class="focus-block">
          <span class="section-label reveal">

            {{ content[lang].focusTitle }}
          </span>

          <div class="focus-list">
            <article
              v-for="(area, i) in content[lang].areas"
              :key="area.number"
              class="focus-item reveal"
              :style="{ '--d': `${0.08 + i * 0.1}s` }"
            >
              <span class="focus-number">{{ area.number }}</span>

              <div class="focus-content">
                <h3>{{ area.title }}</h3>
                <p>{{ area.description }}</p>
              </div>

              <span class="focus-arrow" aria-hidden="true">↗</span>
            </article>
          </div>
        </div>

        <div class="education-block">
          <span class="section-label reveal">

            {{ content[lang].educationTitle }}
          </span>

          <div class="education-list">
            <article
              v-for="(education, index) in content[lang].educations"
              :key="education.institution + index"
              class="education-card reveal"
            >
              <div class="education-icon" aria-hidden="true">EDU.</div>

              <div class="education-info">
                <h3>{{ education.degree }}</h3>

                <a
                  :href="education.url"
                  target="_blank"
                  rel="noopener noreferrer"
                  class="institution-link"
                >
                  {{ education.institution }}
                  <span aria-hidden="true">↗</span>
                </a>

                <p class="education-location">{{ education.location }}</p>

                <span v-if="education.period" class="education-period">
                  {{ education.period }}
                </span>

                <p v-if="education.description" class="education-description">
                  {{ education.description }}
                </p>
              </div>
            </article>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>

<style scoped>
.about-section {
  --accent: var(--color-accent, #e8a45c);
  position: relative;
  min-height: 100vh;
  padding: 110px 0;
  color: #fff;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.about-container {
  width: 100%;
  max-width: 1400px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1.1fr 0.9fr;
  column-gap: clamp(40px, 6vw, 100px);
  align-items: start;
}

/* Apparition au scroll */
.reveal {
  opacity: 0;
  transform: translateY(22px);
  transition: opacity 0.7s ease, transform 0.7s cubic-bezier(0.2, 0.7, 0.2, 1);
  transition-delay: var(--d, 0s);
}

.reveal.visible {
  opacity: 1;
  transform: none;
}

/* Label de section */
.section-label {
  display: flex;
  align-items: center;
  gap: 12px;
  color: var(--accent);
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 2.5px;
}

/* Colonne gauche */
.about-intro {
  position: sticky;
  top: 110px;
}

.about-intro h2 {
  max-width: 620px;
  margin-top: 28px;
  font-size: clamp(36px, 4.5vw, 64px);
  line-height: 1.08;
  letter-spacing: -0.035em;
  font-weight: 700;
  background-clip: text;
  color: #fff; /* repli */
}

.about-intro h3 {
  margin-top: 26px;
  font-size: 19px;
  font-weight: 600;
  line-height: 1.5;
  color: var(--accent);
}

.about-description {
  margin-top: 22px;
  max-width: 600px;
}

.about-description p {
  margin-bottom: 16px;
  font-size: 14.5px;
  line-height: 1.9;
  color: #a0a0a0;
}

/* Bouton CV */
.about-button {
  display: inline-flex;
  align-items: center;
  gap: 14px;
  margin-top: 18px;
  padding: 14px 14px 14px 26px;
  border: 1px solid rgba(255, 255, 255, 0.18);
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.03);
  color: #fff;
  text-decoration: none;
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 0.8px;
  transition: background 0.3s, color 0.3s, border-color 0.3s,
    transform 0.3s, box-shadow 0.3s;
}

.about-button .arrow {
  display: grid;
  place-items: center;
  width: 32px;
  height: 32px;
  border-radius: 50%;
  background: var(--accent);
  color: #111;
  font-size: 16px;
  transition: transform 0.3s;
}

.about-button:hover {
  border-color: var(--accent);
  transform: translateY(-2px);
}

.about-button:hover .arrow {
  transform: translateY(2px);
}

/* Domaines */
.focus-list {
  margin-top: 22px;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.focus-item {
  position: relative;
  display: grid;
  grid-template-columns: 44px 1fr 24px;
  gap: 16px;
  align-items: start;
  padding: 24px 22px;
  border-radius: 18px;
  background: rgba(255, 255, 255, 0.025);
  border: 1px solid rgba(255, 255, 255, 0.07);
  transition: opacity 0.7s ease, transform 0.3s, background 0.3s,
    border-color 0.3s;
}

.focus-item.visible:hover {
  transform: translateX(6px);
  background: rgba(232, 164, 92, 0.06);
  border-color: rgba(232, 164, 92, 0.35);
}

.focus-number {
  font-size: 22px;
  font-weight: 700;
  line-height: 1;
  color: transparent;
  -webkit-text-stroke: 1px var(--accent);
  padding-top: 2px;
}

.focus-content h3 {
  font-size: 17px;
  font-weight: 600;
}

.focus-content p {
  margin-top: 8px;
  font-size: 13px;
  line-height: 1.7;
  color: #8c8c8c;
}

.focus-arrow {
  font-size: 18px;
  color: #555;
  transition: color 0.3s, transform 0.3s;
}

.focus-item:hover .focus-arrow {
  color: var(--accent);
  transform: translate(3px, -3px);
}

/* Formation */
.education-block {
  margin-top: 50px;
}

.education-list {
  margin-top: 22px;
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.education-card {
  display: flex;
  align-items: flex-start;
  gap: 20px;
  padding: 22px;
  border-radius: 18px;
  background: linear-gradient(
    135deg,
    rgba(255, 255, 255, 0.05),
    rgba(255, 255, 255, 0.015)
  );
  border: 1px solid rgba(255, 255, 255, 0.08);
  transition: opacity 0.7s ease, border-color 0.3s;
}

.education-card:hover {
  border-color: rgba(232, 164, 92, 0.35);
}

.education-icon {
  display: grid;
  place-items: center;
  width: 55px;
  height: 55px;
  flex-shrink: 0;
  border-radius: 14px;
  background: rgba(232, 164, 92, 0.12);
  border: 1px solid rgba(232, 164, 92, 0.25);
  color: var(--accent);
  font-size: 12px;
  font-weight: 700;
}

.education-info h3 {
  font-size: 15px;
  font-weight: 600;
  color: #fff;
}

.institution-link {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  margin-top: 8px;
  color: var(--accent);
  font-size: 13px;
  text-decoration: none;
  transition: color 0.3s;
}

.institution-link:hover {
  color: #fff;
}

.education-location {
  margin-top: 6px;
  color: #808080;
  font-size: 12px;
}

.education-period {
  display: block;
  margin-top: 6px;
  color: #999;
  font-size: 11px;
}

.education-description {
  margin-top: 12px;
  color: #808080;
  font-size: 12px;
  line-height: 1.7;
}

/* Accessibilité (focus clavier) */
.about-button:focus-visible,
.institution-link:focus-visible {
  outline: 2px solid var(--accent);
  outline-offset: 3px;
}

/* Responsive */
@media (max-width: 1000px) {
  .about-section {
    padding-left: 5%;
    padding-right: 5%;
  }
}

@media (max-width: 768px) {
  .about-section {
    padding-top: 80px;
    padding-bottom: 80px;
  }

  .about-container {
    grid-template-columns: 1fr;
    row-gap: 60px;
  }

  .about-intro {
    position: static;
  }

  .about-intro h2 {
    font-size: clamp(36px, 8vw, 54px);
  }

  .about-intro h3 {
    font-size: 17px;
  }

  .education-block {
    margin-top: 40px;
  }
}

@media (max-width: 400px) {
  .about-description p {
    font-size: 13px;
  }

  .focus-item {
    padding: 18px 16px;
    gap: 12px;
  }

  .focus-content h3 {
    font-size: 15px;
  }

  .education-card {
    padding: 15px;
    gap: 12px;
  }
}

@media (prefers-reduced-motion: reduce) {
  .reveal {
    opacity: 1;
    transform: none;
    transition: none;
  }

  * {
    transition: none !important;
  }
}
</style>