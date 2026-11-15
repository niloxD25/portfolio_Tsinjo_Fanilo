<script setup>
import { ref, reactive, onMounted, onBeforeUnmount } from 'vue'

defineProps({
  lang: {
    type: String,
    default: 'fr'
  }
})

const ICON_BASE = 'https://cdn.jsdelivr.net/gh/devicons/devicon@v2.16.0/icons'
const iconUrl = (icon) => `${ICON_BASE}/${icon}/${icon}-original.svg`

const tech = {
  html: { name: 'HTML5', icon: 'html5' },
  css: { name: 'CSS3', icon: 'css3' },
  js: { name: 'JavaScript', icon: 'javascript' },
  vue: { name: 'Vue.js', icon: 'vuejs' },
  react: { name: 'React.js', icon: 'react' },

  php: { name: 'PHP', icon: 'php' },
  laravel: { name: 'Laravel', icon: 'laravel' },
  java: { name: 'Java', icon: 'java' },
  spring: { name: 'Spring Boot', icon: 'spring' },
  csharp: { name: 'C#', icon: 'csharp' },
  python: { name: 'Python', icon: 'python' },

  postgres: { name: 'PostgreSQL', icon: 'postgresql' },
  mysql: { name: 'MySQL', icon: 'mysql' },
  oracle: { name: 'Oracle', icon: 'oracle' },

  xd: { name: 'Adobe XD', icon: 'xd' },
  photoshop: { name: 'Adobe Photoshop', icon: 'photoshop' },
  illustrator: { name: 'Adobe Illustrator', icon: 'illustrator' },
  indesign: { name: 'Adobe InDesign', icon: 'indesign', abbr: 'Id' },
  figma: { name: 'Figma', icon: 'figma' },

  kobo: { name: 'KoboToolbox', abbr: 'Ko' },
  mwater: { name: 'mWater', abbr: 'mW' },
  excel: { name: 'Microsoft Excel', abbr: 'XL' }
}

const content = {
  fr: {
    eyebrow: 'MES COMPÉTENCES',
    title: 'Les outils derrière mes solutions.',
    introduction:
      'Un ensemble de technologies et d’outils que j’utilise pour concevoir, développer et faire évoluer des solutions numériques.',
    categories: [
      {
        number: '01',
        title: 'Développement Frontend',
        description: 'Créer des interfaces modernes, intuitives et adaptatives.',
        skills: ['html', 'css', 'js', 'vue', 'react']
      },
      {
        number: '02',
        title: 'Développement Backend',
        description: 'Développer la logique métier et des applications robustes.',
        skills: ['php', 'laravel', 'java', 'spring', 'csharp', 'python']
      },
      {
        number: '03',
        title: 'Bases de données & Data',
        description: 'Structurer, gérer et exploiter efficacement les données.',
        skills: ['postgres', 'mysql', 'oracle']
      },
      {
        number: '04',
        title: 'Outils de Design',
        description: 'Conception graphique, prototypage et création d’interfaces utilisateur.',
        skills: ['figma', 'xd', 'photoshop', 'illustrator', 'indesign']
      },
      {
        number: '05',
        title: 'Collecte & Analyse de Données',
        description: 'Collecte sur le terrain, traitement, analyse et visualisation des données.',
        skills: ['kobo', 'mwater', 'excel', 'python']
      }
    ]
  },

  en: {
    eyebrow: 'MY SKILLS',
    title: 'The tools behind my solutions.',
    introduction:
      'A set of technologies and tools I use to design, develop and improve digital solutions.',
    categories: [
      {
        number: '01',
        title: 'Frontend Development',
        description: 'Building modern, intuitive and responsive interfaces.',
        skills: ['html', 'css', 'js', 'vue', 'react']
      },
      {
        number: '02',
        title: 'Backend Development',
        description: 'Developing business logic and robust applications.',
        skills: ['php', 'laravel', 'java', 'spring', 'csharp', 'python']
      },
      {
        number: '03',
        title: 'Database & Data Management',
        description: 'Structuring, managing and making effective use of data.',
        skills: ['postgres', 'mysql', 'oracle']
      },
      {
        number: '04',
        title: 'Design Tools',
        description: 'Graphic design, prototyping and user interface design.',
        skills: ['figma', 'xd', 'photoshop', 'illustrator', 'indesign']
      },
      {
        number: '05',
        title: 'Data Collection & Analysis',
        description: 'Field data collection, processing, analysis and visualization.',
        skills: ['kobo', 'mwater', 'excel', 'python']
      }
    ]
  }
}

const failed = reactive({})

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

onBeforeUnmount(() => observer?.disconnect())
</script>

<template>
  <section id="skills" ref="root" class="skills-section">
    <div class="skills-container">

      <div class="skills-header">
        <span class="section-label reveal">
          {{ content[lang].eyebrow }}
        </span>

        <div class="skills-heading">
          <h2 class="reveal" style="--d: 0.08s">{{ content[lang].title }}</h2>
          <p class="reveal" style="--d: 0.16s">{{ content[lang].introduction }}</p>
        </div>
      </div>

      <div class="skills-grid">
        <article
          v-for="(category, i) in content[lang].categories"
          :key="category.number"
          class="skill-card reveal"
          :style="{ '--d': `${i * 0.08}s` }"
          @mousemove="onMove"
        >
          <div class="skill-card-top">
            <span class="skill-number">{{ category.number }}</span>
          </div>

          <div class="skill-card-content">
            <h3>{{ category.title }}</h3>
            <p>{{ category.description }}</p>
          </div>

          <ul class="skill-tags">
            <li v-for="id in category.skills" :key="id" class="skill-tag">
              <img
                v-if="tech[id].icon && !failed[id]"
                class="tag-icon"
                :src="iconUrl(tech[id].icon)"
                alt=""
                width="18"
                height="18"
                loading="lazy"
                decoding="async"
                @error="failed[id] = true"
              />
              <span v-else class="tag-fallback" aria-hidden="true">
                {{ tech[id].abbr || tech[id].name.slice(0, 2) }}
              </span>
              {{ tech[id].name }}
            </li>
          </ul>
        </article>
      </div>

    </div>
  </section>
</template>

<style scoped>
.skills-section {
  --accent: var(--color-accent, #e8a45c);
  color: #fff;
  padding: 120px 7%;
}

.skills-container {
  max-width: 1400px;
  margin: 0 auto;
}

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
.skills-heading {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  gap: 40px;
  margin: 28px 0 55px;
}

.skills-heading h2 {
  max-width: 650px;
  font-size: clamp(36px, 5vw, 65px);
  line-height: 1.08;
  font-weight: 700;
  letter-spacing: -0.035em;
  background-clip: text;
  color: #fff; /* repli */
}

.skills-heading p {
  max-width: 390px;
  color: #a0a0a0;
  font-size: 14.5px;
  line-height: 1.8;
}

/* Grille bento : 3 + 3 puis 2 + 2 + 2 */
.skills-grid {
  display: grid;
  grid-template-columns: repeat(6, minmax(0, 1fr));
  gap: 16px;
}

.skill-card {
  --mx: 50%;
  --my: 0%;
  position: relative;
  grid-column: span 2;
  min-height: 260px;
  padding: 28px;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  border-radius: 22px;
  background: linear-gradient(
    145deg,
    rgba(255, 255, 255, 0.05),
    rgba(255, 255, 255, 0.015)
  );
  border: 1px solid rgba(255, 255, 255, 0.08);
  transition: border-color 0.3s, transform 0.3s;
}

.skill-card:nth-child(-n + 2) {
  grid-column: span 3;
}

.skill-card > * {
  position: relative;
}

.skill-card:hover {
  border-color: rgba(232, 164, 92, 0.4);
  transform: translateY(-4px);
}

.skill-card:hover::before {
  opacity: 1;
}

.skill-card-top {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.skill-number {
  font-size: 26px;
  font-weight: 700;
  line-height: 1;
  color: transparent;
  -webkit-text-stroke: 1px var(--accent);
}

.skill-decoration {
  color: #555;
  font-size: 20px;
  transition: color 0.3s, transform 0.3s;
}

.skill-card:hover .skill-decoration {
  color: var(--accent);
  transform: translate(3px, -3px);
}

.skill-card-content {
  margin: 24px 0;
}

.skill-card-content h3 {
  margin-bottom: 10px;
  font-size: 21px;
  font-weight: 600;
  letter-spacing: -0.01em;
}

.skill-card-content p {
  color: #8f8f8f;
  font-size: 13.5px;
  line-height: 1.7;
}

/* Tags avec icônes */
.skill-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin: auto 0 0;
  padding: 0;
  list-style: none;
}

.skill-tag {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 7px 14px 7px 9px;
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.09);
  color: #d0d0d0;
  font-size: 12px;
  font-weight: 500;
  transition: transform 0.25s, background 0.25s, border-color 0.25s,
    color 0.25s;
}

.skill-tag:hover {
  transform: translateY(-2px);
  background: rgba(232, 164, 92, 0.1);
  border-color: rgba(232, 164, 92, 0.5);
  color: #fff;
}

.tag-icon {
  width: 18px;
  height: 18px;
  flex-shrink: 0;
  object-fit: contain;
}

.tag-fallback {
  display: grid;
  place-items: center;
  min-width: 20px;
  height: 18px;
  padding: 0 3px;
  flex-shrink: 0;
  border-radius: 5px;
  background: rgba(232, 164, 92, 0.15);
  color: var(--accent);
  font-size: 9px;
  font-weight: 700;
  letter-spacing: 0.2px;
}

/* Tablette */
@media (max-width: 900px) {
  .skills-section {
    padding: 90px 6%;
  }

  .skills-heading {
    flex-direction: column;
    align-items: flex-start;
    gap: 20px;
  }

  .skills-heading p {
    max-width: 600px;
  }

  .skills-grid {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }

  .skill-card,
  .skill-card:nth-child(-n + 2) {
    grid-column: span 1;
  }

  .skill-card:last-child:nth-child(odd) {
    grid-column: 1 / -1;
  }
}

/* Mobile */
@media (max-width: 600px) {
  .skills-section {
    padding: 75px 6%;
  }

  .skills-heading {
    margin: 25px 0 35px;
  }

  .skills-heading h2 {
    font-size: 38px;
  }

  .skills-grid {
    grid-template-columns: 1fr;
    gap: 14px;
  }

  .skill-card,
  .skill-card:last-child:nth-child(odd) {
    grid-column: auto;
    min-height: 230px;
    padding: 24px;
  }

  .skill-card-content h3 {
    font-size: 19px;
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