<template>

    <footer class="hero-footer">
        <div class="hero-footer">
            <span>Based in Antananarivo, Madagascar</span>
            <span>© {{ new Date().getFullYear() }}</span>
        </div>
    </footer>

</template>

<style scoped>
.hero-footer {
  position: relative;
  z-index: 4;
  width: 100%;
  margin-top: auto;
  padding-top: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: #777;
  font-size: 9px;
  letter-spacing: 1.5px;
  flex-shrink: 0;
}

@media (max-width: 600px) {
  .hero-footer {
    font-size: 8px;
    letter-spacing: 1px;
  }
}
</style>