
<script setup>
defineProps({
  lang: {
    type: String,
    default: 'fr'
  }
})

const content = {
  fr: {
    role: 'Développeur Full-stack',
    name: 'Tsinjo Fanilo'
  },
  en: {
    role: 'Full-stack Developer',
    name: 'Tsinjo Fanilo'
  }
}
</script>

<template>
  <main class="hero">

    <div class="title-block">
      <div class="identity">
        <h1>{{ content[lang].name }}</h1>
        <p>{{ content[lang].role }}</p>
      </div>

      <div class="background-word">
        PORTFOLIO
      </div>
    </div>

    <img
      src="/images/illustration_me_wb.png"
      alt="Portrait de Tsinjo Fanilo"
      class="portrait"
    />

  </main>
</template>

<style scoped>
.hero {
  min-height: 100vh;
  min-height: 100svh;
  position: relative;
  overflow: hidden;
  display: flex;
  flex-direction: column;
}

.title-block {
  position: absolute;
  top: 35%;
  left: 0;
  width: 100%;
  transform: translateY(-50%);
  padding: 0 7%;
}

.identity {
  position: relative;
  z-index: 2;
}

.identity h1 {
  font-size: clamp(38px, 18vw, 58px);
  font-weight: 700;
  color: #b3b1b1;
}

.identity p {
  margin-left: 12px;
  font-size: 16px;
  font-weight: 600;
  color: #b3b1b1;
}

.background-word {
  position: relative;
  z-index: 1;
  width: 100%;
  margin-top: 80px;
  font-size: clamp(90px, 19vw, 280px);
  font-weight: 700;
  line-height: 0.85;
  color: #222222;
  white-space: normal;
  overflow-wrap: anywhere;
  word-break: normal;
  pointer-events: none;
}

.portrait {
  position: absolute;
  z-index: 2;
  bottom: 0;
  right: 5%;
  height: 75%;
  max-width: 60%;
  object-fit: contain;
  pointer-events: none;
}

@media (max-width: 768px) {
  .title-block {
    top: 30%;
    padding: 0 6%;
  }

  .background-word {
    font-size: clamp(90px, 19vw, 145px);
  }

  .identity {
    margin-top: 25px;
  }

  .identity p {
    font-size: 10px;
  }
}

@media (max-width: 600px) {
  .hero {
    padding: 20px 6%;
  }

  .portrait {
    height: 48%;
    max-width: 85%;
    right: 7%;
  }
}
</style>
