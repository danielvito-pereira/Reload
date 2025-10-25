<template>
  <section class="portifolio">
    <tituloH1>PORTFÓLIO</tituloH1>
    <carroselCards :items="cases" title="Nosso Trabalho" />
  </section>
</template>

<script setup>
  import tituloH1 from '@/components/TituloH1.vue'
  import carroselCards from '@/components/CarroselCards.vue'
</script>

<style lang="scss" scoped >
  .portifolio{
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: aqua;
  }
</style>
