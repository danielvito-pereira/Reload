<template>
  <div class="footer-logo">
    <RouterLink to="/">
      <img src="/src/components/icons/Logo_Foter.svg" alt="Logo da empresa" />
    </RouterLink>
  </div>
</template>

<style scoped lang="scss">
.footer-logo {
  img {
    width: 12.5rem;
    height: auto;
    transition: transform 0.3s ease;
  }

  &:hover img {
    transform: scale(1.05);
  }
}
</style>
