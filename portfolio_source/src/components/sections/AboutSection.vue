
<script setup>
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
    education: 'FORMATION',
    button: 'DÉCOUVRIR MES PROJETS'
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
    education: 'EDUCATION',
    button: 'EXPLORE MY PROJECTS'
  }
}
</script>

<template>
  <section id="about" class="about-section">

    <div class="about-container">

      <!-- LEFT COLUMN -->
      <div class="about-intro">

        <span class="section-label">
          <span class="label-line"></span>
          {{ content[lang].eyebrow }}
        </span>

        <h2>
          {{ content[lang].title }}
        </h2>

        <h3>
          {{ content[lang].introduction }}
        </h3>

        <div class="about-description">
          <p
            v-for="paragraph in content[lang].paragraphs"
            :key="paragraph"
          >
            {{ paragraph }}
          </p>
        </div>

        <a href="#projects" class="about-button">
          {{ content[lang].button }}
          <span>↗</span>
        </a>

      </div>

      <!-- RIGHT COLUMN -->
      <div class="about-details">

        <div class="focus-block">

          <span class="section-label">
            <span class="label-line"></span>
            {{ content[lang].focusTitle }}
          </span>

          <article
            v-for="area in content[lang].areas"
            :key="area.number"
            class="focus-item"
          >
            <span class="focus-number">
              {{ area.number }}
            </span>

            <div class="focus-content">
              <h3>{{ area.title }}</h3>
              <p>{{ area.description }}</p>
            </div>

          </article>

        </div>

        
        <div class="education-block">

        <span class="section-label">
            <span class="label-line"></span>
            {{ content[lang].educationsTitle }}
        </span>

        <div class="education-list">

            <article
            v-for="(education, index) in content[lang].educations"
            :key="education.institution + index"
            class="education-content"
            >
            <div class="education-icon">
                EDU.
            </div>

            <div class="education-info">

                <h3>{{ education.degree }}</h3>

                <a
                :href="education.url"
                target="_blank"
                rel="noopener noreferrer"
                class="institution-link"
                >
                {{ education.institution }}
                <span>↗</span>
                </a>

                <p>{{ education.location }}</p>

                <span v-if="education.period">
                {{ education.period }}
                </span>

                <p
                v-if="education.description"
                class="education-description"
                >
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
  position: relative;
  min-height: 100vh;
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
  align-items: center;
}

.section-label {
  display: flex;
  align-items: center;
  gap: 12px;
  color: var(--color-accent);
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 2px;
}

.label-line {
  width: 28px;
  height: 1px;
  background: var(--color-accent);
}

.about-intro h2 {
  max-width: 600px;
  margin-top: 30px;
  font-size: clamp(36px, 4.5vw, 64px);
  line-height: 1.12;
  letter-spacing: -2px;
  font-weight: 700;
}

.about-intro h3 {
  margin-top: 28px;
  font-size: 19px;
  font-weight: 600;
  line-height: 1.5;
  color: var(--color-accent);
}

.about-description {
  margin-top: 22px;
  max-width: 600px;
}

.about-description p {
  margin-bottom: 17px;
  font-size: 14px;
  line-height: 1.9;
  color: #999;
}

.about-button {
  display: inline-flex;
  align-items: center;
  gap: 30px;
  margin-top: 20px;
  padding: 15px 20px;
  border: 1px solid #555;
  color: #fff;
  text-decoration: none;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 1px;
  transition: all .3s;
}

.about-button:hover {
  background: var(--color-accent);
  color: #111;
  border-color: var(--color-accent);
}

.about-button span {
  font-size: 18px;
}

.focus-block {
  width: 100%;
}

.focus-item {
  display: grid;
  grid-template-columns: 35px 1fr 20px;
  gap: 15px;
  align-items: start;
  padding: 25px 0;
  border-bottom: 1px solid #333;
}

.focus-item:first-of-type {
  margin-top: 15px;
}

.focus-number {
  font-size: 12px;
  color: var(--color-accent);
  padding-top: 4px;
}

.focus-content h3 {
  font-size: 17px;
  font-weight: 600;
}

.focus-content p {
  margin-top: 9px;
  font-size: 12px;
  line-height: 1.7;
  color: #888;
}

.education-block {
  margin-top: 55px;
}

.education-content {
  display: flex;
  align-items: center;
  gap: 20px;
  margin-top: 22px;
  padding: 22px;
  background: #202020;
  border: 1px solid #303030;
}

.education-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 55px;
  height: 55px;
  flex-shrink: 0;
  background: #29241e;
  color: var(--color-accent);
  font-size: 12px;
  font-weight: 700;
}

.education-content h3 {
  font-size: 15px;
  font-weight: 600;
}

.education-content p {
  margin-top: 7px;
  color: var(--color-accent);
  font-size: 13px;
}

.education-content span {
  display: block;
  margin-top: 5px;
  color: #777;
  font-size: 11px;
}


.education-list {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.education-content {
  display: flex;
  align-items: flex-start;
  gap: 20px;
  padding: 22px;
  background: #202020;
  border: 1px solid #303030;
  transition: border-color .3s;
}

.education-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 55px;
  height: 55px;
  flex-shrink: 0;
  background: #29241e;
  color: var(--color-accent);
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
  gap: 7px;
  margin-top: 8px;
  color: var(--color-accent);
  font-size: 13px;
  text-decoration: none;
  transition: color .3s;
}

.institution-link:hover {
  color: #fff;
}

.institution-link span {
  font-size: 14px;
}

.education-info p {
  margin-top: 7px;
  color: #777;
  font-size: 11px;
}

.education-info > span {
  display: block;
  margin-top: 6px;
  color: #999;
  font-size: 11px;
}

.education-info .education-description {
  margin-top: 12px;
  line-height: 1.7;
}


@media (max-width: 1000px) {
  .about-section {
    padding-left: 5%;
    padding-right: 5%;
  }
}

@media (max-width: 768px) {
  .about-container {
    grid-template-columns: 1fr;
    gap: 65px;
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

  .about-index {
    padding-top: 55px;
  }
}

@media (max-width: 400px) {
  .about-description p {
    font-size: 13px;
  }

  .focus-content h3 {
    font-size: 15px;
  }

  .education-content {
    padding: 15px;
    gap: 12px;
  }
}
</style>
