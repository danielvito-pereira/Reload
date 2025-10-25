<template>
  <section class="base-section">
    <div class="container">
      <slot />
    </div>
  </section>
</template>

<script setup>
// Nenhuma lógica por enquanto — é um container visual genérico
</script>

<style scoped lang="scss">
.base-section {
  width: 100%;
  padding: 4rem 1.5rem; // espaçamento vertical padrão
  display: flex;
  justify-content: center;

  .container {
    width: 100%;
    max-width: 1200px; // largura típica de landing pages
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 3rem;
  }

  // Responsividade
  @media (max-width: 768px) {
    padding: 3rem 1rem;
  }

  @media (max-width: 480px) {
    padding: 2rem 1rem;
  }
}
</style>
