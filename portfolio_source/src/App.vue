
<script setup>
import { ref } from 'vue'

import MainNavbar from './components/layout/MainNavbar.vue'
import Footer from './components/layout/Footer.vue'

import HeroSection from './components/sections/HeroSection.vue'
import AboutSection from './components/sections/AboutSection.vue'

const lang = ref('fr')
</script>

<template>
  <MainNavbar
    :lang="lang"
    @change-language="lang = $event"
  />

  <HeroSection :lang="lang" />

  <AboutSection :lang="lang" />

  <Footer />
</template>
