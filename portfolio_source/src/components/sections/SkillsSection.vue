
<script setup>
defineProps({
  lang: {
    type: String,
    default: 'fr'
  }
})

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
            skills: ['HTML5', 'CSS3', 'JavaScript', 'Vue.js', 'React.js']
        },
        {
            number: '02',
            title: 'Développement Backend',
            description: 'Développer la logique métier et des applications robustes.',
            skills: ['PHP', 'Laravel', 'Java', 'Spring Boot', 'C#', 'Python']
        },
        {
            number: '03',
            title: 'Bases de données & Data',
            description: 'Structurer, gérer et exploiter efficacement les données.',
            skills: ['PostgreSQL', 'MySQL', 'SQL', 'Oracle']
        },
        {
            number: '04',
            title: 'Outils de Design',
            description: 'Conception graphique, prototypage et création d’interfaces utilisateur.',
            skills: ['Adobe XD', 'Adobe Photoshop', 'Adobe Illustrator', 'Adobe InDesign', 'Figma']
        },
        {
            number: '05',
            title: 'Collecte & Analyse de Données',
            description: 'Collecte sur le terrain, traitement, analyse et visualisation des données.',
            skills: ['KoboToolbox', 'mWater', 'Microsoft Excel', 'Python']
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
        skills: ['HTML5', 'CSS3', 'JavaScript', 'Vue.js', 'React.js']
      },
      {
        number: '02',
        title: 'Backend Development',
        description: 'Developing business logic and robust applications.',
        skills: ['PHP', 'Laravel', 'Java', 'Spring Boot', 'C#']
      },
      {
        number: '03',
        title: 'Database & Data Management',
        description: 'Structuring, managing and making effective use of data.',
        skills: ['PostgreSQL', 'MySQL', 'SQL', 'KoboToolbox']
      },
      {
        number: '04',
        title: 'Design Tools',
        description: 'Graphic design, prototyping and user interface design.',
        skills: ['Adobe XD', 'Adobe Photoshop', 'Adobe Illustrator', 'Adobe InDesign', 'Figma']
        },
        {
        number: '05',
        title: 'Data Collection & Analysis',
        description: 'Field data collection, processing, analysis and visualization.',
        skills: ['KoboToolbox', 'mWater', 'Microsoft Excel', 'Python']
        }
    ]
  }
}
</script>

<template>
  <section id="skills" class="skills-section">
    <div class="skills-container">

      <div class="skills-header">
        <span class="section-label">
          <span class="label-line"></span>
          {{ content[lang].eyebrow }}
        </span>

        <div class="skills-heading">
          <h2>{{ content[lang].title }}</h2>
          <p>{{ content[lang].introduction }}</p>
        </div>
      </div>

      <div class="skills-grid">
        <article
          v-for="category in content[lang].categories"
          :key="category.number"
          class="skill-card"
        >
          <div class="skill-card-top">
            <span class="skill-number">{{ category.number }}</span>
          </div>

          <div class="skill-card-content">
            <h3>{{ category.title }}</h3>
            <p>{{ category.description }}</p>
          </div>

          <div class="skill-tags">
            <span
              v-for="skill in category.skills"
              :key="skill"
              class="skill-tag"
            >
              {{ skill }}
            </span>
          </div>
        </article>
      </div>

    </div>
  </section>
</template>

<style scoped>
.skills-section {
  color: #fff;
  padding: 120px 7%;
}

.skills-container {
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
  display: inline-block;
  width: 30px;
  height: 1px;
  background: var(--color-accent);
}

.skills-heading {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  gap: 40px;
  margin: 30px 0 55px;
}

.skills-heading h2 {
  max-width: 650px;
  font-size: clamp(36px, 5vw, 65px);
  line-height: 1.1;
  font-weight: 600;
  letter-spacing: -2px;
}

.skills-heading p {
  max-width: 390px;
  color: #999;
  font-size: 14px;
  line-height: 1.8;
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 18px;
}

.skill-card {
  min-height: 260px;
  padding: 30px;
  background: #202020;
  border: 1px solid #303030;
  display: flex;
  flex-direction: column;
  transition: border-color 0.3s, transform 0.3s;
}

.skill-card:hover {
  border-color: var(--color-accent);
  transform: translateY(-4px);
}

.skill-card-top {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.skill-number {
  color: var(--color-accent);
  font-size: 13px;
  font-weight: 600;
}

.skill-decoration {
  color: #666;
  font-size: 20px;
  transition: color 0.3s, transform 0.3s;
}

.skill-card:hover .skill-decoration {
  color: var(--color-accent);
  transform: translate(3px, -3px);
}

.skill-card-content {
  margin: 25px 0;
}

.skill-card-content h3 {
  margin-bottom: 10px;
  font-size: 21px;
  font-weight: 600;
}

.skill-card-content p {
  color: #999;
  font-size: 13px;
  line-height: 1.7;
}

.skill-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 9px;
  margin-top: auto;
}

.skill-tag {
  padding: 8px 13px;
  background: #292929;
  border: 1px solid #383838;
  color: #ccc;
  font-size: 12px;
  transition: all 0.3s;
}

.skill-tag:hover {
  background: var(--color-accent);
  border-color: var(--color-accent);
  color: #171717;
}

/* Tablet */
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
    letter-spacing: -1px;
  }

  .skills-grid {
    grid-template-columns: 1fr;
    gap: 14px;
  }

  .skill-card {
    min-height: 230px;
    padding: 24px;
  }

  .skill-card-content h3 {
    font-size: 19px;
  }
}
</style>
