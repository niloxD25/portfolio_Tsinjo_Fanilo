<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

defineProps({
  lang: {
    type: String,
    default: 'fr'
  }
})

defineEmits(['change-language'])

const navItems = [
  { id: 'about', label: { fr: 'À propos', en: 'About' } },
  { id: 'skills', label: { fr: 'Compétences', en: 'Skills' } },
  { id: 'projects', label: { fr: 'Projets', en: 'Projects' } },
  { id: 'contact', label: { fr: 'Contact', en: 'Contact' } }
]

const open = ref(false)
const scrolled = ref(false)
const active = ref('')

let observer = null

const onScroll = () => {
  scrolled.value = window.scrollY > 10
}

const onKeydown = (e) => {
  if (e.key === 'Escape') open.value = false
}

onMounted(() => {
  onScroll()
  window.addEventListener('scroll', onScroll, { passive: true })
  window.addEventListener('keydown', onKeydown)

  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) active.value = entry.target.id
      })
    },
    { rootMargin: '-45% 0px -50% 0px' }
  )
  navItems.forEach(({ id }) => {
    const el = document.getElementById(id)
    if (el) observer.observe(el)
  })
})

onBeforeUnmount(() => {
  window.removeEventListener('scroll', onScroll)
  window.removeEventListener('keydown', onKeydown)
  observer?.disconnect()
})
</script>

<template>
  <header class="navbar" :class="{ scrolled, open }">
    <div class="bar">
      <a href="#" class="logo" aria-label="Accueil">TF<span>.</span></a>

      <nav
        id="main-nav"
        class="nav"
        :class="{ open }"
        aria-label="Navigation principale"
      >
        <a
          v-for="item in navItems"
          :key="item.id"
          :href="`#${item.id}`"
          :class="{ active: active === item.id }"
          @click="open = false"
        >
          {{ item.label[lang] }}
        </a>
      </nav>

      <div class="actions">
        <button
          class="lang"
          role="switch"
          :aria-checked="lang === 'en'"
          :aria-label="lang === 'fr' ? 'Switch to English' : 'Passer en français'"
          @click="$emit('change-language', lang === 'fr' ? 'en' : 'fr')"
        >
          <span class="thumb" :class="{ right: lang === 'en' }"></span>
          <span class="opt" :class="{ on: lang === 'fr' }">FR</span>
          <span class="opt" :class="{ on: lang === 'en' }">EN</span>
        </button>

        <button
          class="burger"
          :class="{ open }"
          :aria-expanded="open"
          aria-controls="main-nav"
          aria-label="Menu"
          @click="open = !open"
        >
          <span></span>
          <span></span>
        </button>
      </div>
    </div>
  </header>
</template>

<style scoped>
.navbar {
  --accent: var(--color-accent, #e8a45c);
  position: sticky;
  top: 16px;
  z-index: 50;
  width: 100%;
  flex-shrink: 0;
}

.bar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 20px;
  padding: 10px 12px 10px 24px;
  transition: background 0.3s, box-shadow 0.3s, border-color 0.3s;
}

/* Logo */
.logo {
  font-size: 26px;
  font-weight: 700;
  letter-spacing: -0.5px;
  color: #fff;
  text-decoration: none;
  flex-shrink: 0;
}

.logo span {
  color: var(--accent);
}

/* Navigation */
.nav {
  display: flex;
  align-items: center;
  gap: clamp(4px, 1.5vw, 12px);
}

.nav a {
  position: relative;
  padding: 8px 14px;
  font-size: 13px;
  font-weight: 500;
  color: #b5b5b5;
  text-decoration: none;
  white-space: nowrap;
  border-radius: 999px;
  transition: color 0.25s, background 0.25s;
}

.nav a::after {
  content: '';
  position: absolute;
  left: 50%;
  bottom: 3px;
  width: 4px;
  height: 4px;
  border-radius: 50%;
  background: var(--accent);
  transform: translateX(-50%) scale(0);
  transition: transform 0.25s;
}

.nav a:hover {
  color: #fff;
  background: rgba(255, 255, 255, 0.06);
}

.nav a.active {
  color: #fff;
}

.nav a.active::after {
  transform: translateX(-50%) scale(1);
}

/* Actions */
.actions {
  display: flex;
  align-items: center;
  gap: 10px;
}

/* Sélecteur de langue (bascule) */
.lang {
  position: relative;
  display: grid;
  grid-template-columns: 1fr 1fr;
  padding: 4px;
  border: 1px solid rgba(255, 255, 255, 0.15);
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.04);
  cursor: pointer;
  font-family: inherit;
}

.lang .opt {
  position: relative;
  z-index: 1;
  min-width: 38px;
  padding: 6px 0;
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.5px;
  color: #9a9a9a;
  text-align: center;
  transition: color 0.25s;
}

.lang .opt.on {
  color: #111;
}

.lang .thumb {
  position: absolute;
  top: 4px;
  bottom: 4px;
  left: 4px;
  width: calc(50% - 4px);
  border-radius: 999px;
  background: var(--accent);
  transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.lang .thumb.right {
  transform: translateX(100%);
}

.lang:focus-visible,
.burger:focus-visible,
.nav a:focus-visible,
.logo:focus-visible {
  outline: 2px solid var(--accent);
  outline-offset: 2px;
}

/* Hamburger (caché sur desktop) */
.burger {
  display: none;
  position: relative;
  width: 40px;
  height: 40px;
  border: 1px solid rgba(255, 255, 255, 0.15);
  border-radius: 50%;
  background: transparent;
  cursor: pointer;
}

.burger span {
  position: absolute;
  left: 11px;
  width: 16px;
  height: 2px;
  border-radius: 2px;
  background: #fff;
  transition: transform 0.3s, top 0.3s;
}

.burger span:nth-child(1) { top: 15px; }
.burger span:nth-child(2) { top: 22px; }

.burger.open span:nth-child(1) { top: 18px; transform: rotate(45deg); }
.burger.open span:nth-child(2) { top: 18px; transform: rotate(-45deg); }

/* Mobile / tablette */
@media (max-width: 768px) {
  .navbar {
    top: 10px;
  }

  .bar {
    padding: 8px 8px 8px 18px;
  }

  .burger {
    display: block;
  }

  .nav {
    position: absolute;
    top: calc(100% + 10px);
    left: 0;
    right: 0;
    flex-direction: column;
    align-items: stretch;
    gap: 2px;
    padding: 10px;
    border-radius: 24px;
    background: rgba(15, 15, 15, 0.92);
    border: 1px solid rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(16px);
    -webkit-backdrop-filter: blur(16px);
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4);
    opacity: 0;
    visibility: hidden;
    transform: translateY(-8px) scale(0.98);
    transform-origin: top center;
    transition: opacity 0.25s, transform 0.25s, visibility 0.25s;
  }

  .nav.open {
    opacity: 1;
    visibility: visible;
    transform: none;
  }

  .nav a {
    padding: 14px 16px;
    font-size: 15px;
    border-radius: 14px;
  }

  .nav a::after {
    left: auto;
    right: 18px;
    bottom: 50%;
    transform: translateY(50%) scale(0);
  }

  .nav a.active::after {
    transform: translateY(50%) scale(1);
  }
}

@media (prefers-reduced-motion: reduce) {
  * {
    transition: none !important;
  }
}
</style>