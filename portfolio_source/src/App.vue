
<script setup>
import { ref } from 'vue'

import MainNavbar from './components/layout/MainNavbar.vue'
import HeroSection from './components/sections/HeroSection.vue'

const lang = ref('fr')
</script>

<template>
  <MainNavbar
    :lang="lang"
    @change-language="lang = $event"
  />

  <HeroSection :lang="lang" />
</template>
