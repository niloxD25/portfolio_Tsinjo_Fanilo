
<script setup>
import { ref } from 'vue'

import MainNavbar from './components/layout/MainNavbar.vue'
import Footer from './components/layout/Footer.vue'

import HeroSection from './components/sections/HeroSection.vue'
import AboutSection from './components/sections/AboutSection.vue'
import SkillsSection from './components/sections/SkillsSection.vue'
import ContactSection from './components/sections/ContactSection.vue'

const lang = ref('fr')
</script>

<template>
  <MainNavbar
    :lang="lang"
    @change-language="lang = $event"
    class="navbar"
  />

  <HeroSection :lang="lang" />

  <AboutSection :lang="lang" />

  <SkillsSection :lang="lang" />

  <ContactSection :lang="lang" />

  <Footer />
</template>

<style scoped>
  .navbar {
    top: 0;
    z-index: 1000;
    background: #111111;
    height: 80px;
  }
</style>
