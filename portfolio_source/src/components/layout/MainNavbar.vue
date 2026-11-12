
<script setup>
defineProps({
  lang: {
    type: String,
    default: 'fr'
  }
})

defineEmits(['change-language'])

const navItems = {
  fr: ['À propos', 'Compétences', 'Projets', 'Contact'],
  en: ['About', 'Skills', 'Projects', 'Contact']
}
</script>

<template>
  <header class="navbar">
    <a href="#" class="logo">TF<span>.</span></a>

    <nav>
      <a
        v-for="item in navItems[lang]"
        :key="item"
        href="#"
      >
        {{ item }}
      </a>
    </nav>

    <button
      class="language"
      @click="$emit('change-language', lang === 'fr' ? 'en' : 'fr')"
      :aria-label="lang === 'fr' ? 'Switch to English' : 'Passer en français'"
    >
      {{ lang.toUpperCase() }} <span>↗</span>
    </button>
  </header>
</template>

<style scoped>
.navbar {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 25px;
  position: relative;
  z-index: 5;
  flex-shrink: 0;
}

.logo {
  font-size: 30px;
  font-weight: 700;
  color: white;
  text-decoration: none;
  flex-shrink: 0;
}

.logo span {
  color: #e8a45c;
}

.navbar nav {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: clamp(15px, 3vw, 35px);
}

.navbar nav a {
  color: #b5b5b5;
  text-decoration: none;
  font-size: 13px;
  white-space: nowrap;
  transition: color .3s;
}

.navbar nav a:hover {
  color: var(--color-accent);
}

.language {
  display: flex;
  align-items: center;
  gap: 8px;
  background: transparent;
  border: 1px solid #555;
  color: white;
  padding: 10px 17px;
  cursor: pointer;
  border-radius: 30px;
  flex-shrink: 0;
}

@media (max-width: 900px) {
  .navbar {
    gap: 15px;
  }

  .navbar nav {
    gap: 16px;
  }

  .navbar nav a {
    font-size: 11px;
  }

  .logo {
    font-size: 26px;
  }

  .language {
    padding: 8px 12px;
    font-size: 11px;
  }
}

@media (max-width: 600px) {
  .navbar {
    display: grid;
    grid-template-columns: 1fr auto;
    row-gap: 22px;
  }

  .logo {
    font-size: 27px;
  }

  .navbar nav {
    grid-column: 1 / -1;
    grid-row: 2;
    width: 100%;
    justify-content: space-between;
    gap: 8px;
  }

  .navbar nav a {
    font-size: 11px;
  }

  .language {
    grid-column: 2;
    grid-row: 1;
    padding: 8px 12px;
  }
}

@media (max-width: 380px) {
  .navbar nav a {
    font-size: 10px;
  }
}
</style>
