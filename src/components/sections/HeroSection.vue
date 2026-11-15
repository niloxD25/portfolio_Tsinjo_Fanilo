<script setup>
defineProps({
  lang: {
    type: String,
    default: 'fr'
  }
})

const content = {
  fr: {
    greeting: 'Bonjour, je suis',
    role: 'Développeur Full-stack',
    name: 'Tsinjo Fanilo',
    cta: 'Voir mes projets',
    contact: 'Me contacter',
    scroll: 'Défiler'
  },
  en: {
    greeting: "Hi, I'm",
    role: 'Full-stack Developer',
    name: 'Tsinjo Fanilo',
    cta: 'View my projects',
    contact: 'Contact me',
    scroll: 'Scroll'
  }
}
</script>

<template>
  <main class="hero">
    <div class="title-block">
      <div class="identity">

        <p class="greeting">{{ content[lang].greeting }}</p>
        <h1>{{ content[lang].name }}</h1>
        <p class="role">{{ content[lang].role }}</p>

        <div class="actions">
          <a href="#projects" class="btn primary">
            {{ content[lang].cta }} <span>↗</span>
          </a>
          <a href="#contact" class="btn ghost">
            {{ content[lang].contact }}
          </a>
        </div>
      </div>

      <div class="background-word" aria-hidden="true">PORTFOLIO</div>
    </div>

    <img
      src="/images/illustration_me_wb.png"
      alt="Portrait de Tsinjo Fanilo"
      class="portrait"
    />

    <a href="#about" class="scroll" :aria-label="content[lang].scroll">
      <span class="mouse"><i></i></span>
    </a>
  </main>
</template>

<style scoped>
.hero {
  --accent: var(--color-accent, #e8a45c);
  min-height: 100vh;
  min-height: 100svh;
  position: relative;
  overflow: hidden;
  display: flex;
  flex-direction: column;
}

.title-block {
  position: absolute;
  top: 38%;
  left: 0;
  width: 100%;
  transform: translateY(-50%);
  padding: 0 7%;
}

.identity {
  position: relative;
  z-index: 3;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 6px;
}

.greeting {
  font-size: clamp(14px, 2vw, 18px);
  font-weight: 500;
  color: var(--accent);
  animation: rise 0.7s 0.15s both;
}

.identity h1 {
  font-size: clamp(38px, 8vw, 84px);
  font-weight: 700;
  line-height: 1.02;
  letter-spacing: -0.03em;
  background: #fff;
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  color: #e5e5e5;
  animation: rise 0.7s 0.25s both;
}

.role {
  font-size: clamp(15px, 2vw, 20px);
  font-weight: 500;
  color: #b3b1b1;
  animation: rise 0.7s 0.35s both;
}

/* Boutons */
.actions {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  margin-top: 22px;
  animation: rise 0.7s 0.45s both;
}

.btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 12px 22px;
  font-size: 14px;
  font-weight: 600;
  text-decoration: none;
  border-radius: 999px;
}

.btn.primary {
  color: #111;
  background: var(--accent);
}

.btn.primary:hover {
  transform: translateY(-2px);
}

.btn.primary span {
  transition: transform 0.25s;
}

.btn.primary:hover span {
  transform: translate(2px, -2px);
}

.btn.ghost {
  color: #fff;
  border: 1px solid rgba(255, 255, 255, 0.2);
  background: rgba(255, 255, 255, 0.03);
}

.btn.ghost:hover {
  transform: translateY(-2px);
}

.btn:focus-visible {
  outline: 2px solid var(--accent);
  outline-offset: 3px;
}

.background-word {
  position: relative;
  z-index: 1;
  width: 100%;
  margin-top: 70px;
  font-size: clamp(90px, 19vw, 280px);
  font-weight: 800;
  line-height: 0.85;
  letter-spacing: -0.04em;
  color: transparent;
  -webkit-text-stroke: 1.5px rgba(255, 255, 255, 0.09);
  white-space: normal;
  overflow-wrap: anywhere;
  word-break: normal;
  user-select: none;
  pointer-events: none;
  animation: fade 1.2s 0.3s both;
}

/* Portrait */
.portrait {
  position: absolute;
  z-index: 2;
  bottom: 0;
  right: 5%;
  height: 75%;
  max-width: 60%;
  object-fit: contain;
  pointer-events: none;
  filter: drop-shadow(0 20px 40px rgba(0, 0, 0, 0.45));
  animation: slide 1s 0.3s cubic-bezier(0.2, 0.7, 0.2, 1) both;
}

/* Indicateur de défilement */
.scroll {
  position: absolute;
  z-index: 3;
  bottom: 22px;
  left: 7%;
  display: none;
  opacity: 0.7;
  transition: opacity 0.25s;
}

.scroll:hover {
  opacity: 1;
}

.mouse {
  display: block;
  position: relative;
  width: 22px;
  height: 34px;
  border: 1.5px solid rgba(255, 255, 255, 0.4);
  border-radius: 12px;
}

.mouse i {
  position: absolute;
  top: 7px;
  left: 50%;
  width: 3px;
  height: 7px;
  border-radius: 2px;
  background: var(--accent);
  transform: translateX(-50%);
  animation: wheel 1.8s ease-in-out infinite;
}

@media (min-width: 900px) {
  .scroll {
    display: block;
  }
}

/* Animations */
@keyframes rise {
  from {
    opacity: 0;
    transform: translateY(18px);
  }
  to {
    opacity: 1;
    transform: none;
  }
}

@keyframes fade {
  from { opacity: 0; }
  to { opacity: 1; }
}

@keyframes slide {
  from {
    opacity: 0;
    transform: translateX(40px);
  }
  to {
    opacity: 1;
    transform: none;
  }
}

@keyframes breathe {
  0%, 100% { transform: scale(1); opacity: 0.9; }
  50% { transform: scale(1.08); opacity: 1; }
}

@keyframes ping {
  75%, 100% {
    transform: scale(2.4);
    opacity: 0;
  }
}

@keyframes wheel {
  0% { opacity: 0; transform: translate(-50%, 0); }
  30% { opacity: 1; }
  100% { opacity: 0; transform: translate(-50%, 10px); }
}

/* Tablette / mobile */
@media (max-width: 768px) {
  .title-block {
    top: 32%;
    padding: 0 6%;
  }

  .background-word {
    margin-top: 50px;
    font-size: clamp(90px, 19vw, 145px);
    -webkit-text-stroke-width: 1px;
  }

  .btn {
    padding: 10px 18px;
    font-size: 13px;
  }
}

@media (max-width: 600px) {
  .hero {
    padding: 20px 6%;
  }

  .title-block {
    top: 30%;
  }

  .portrait {
    max-width: 85%;
    height: 62%;
    right: 7%;
  }

  .glow {
    width: 90vw;
    right: -10%;
  }
}

@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation: none !important;
    transition: none !important;
  }
}
</style>