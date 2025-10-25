<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import MenuHamburguer from './MenuHamburguer.vue'
import MainBanner from './MainBanner.vue'
import CardsContainer from '../Cards/CardsContainer.vue'
import NavBar from './NavBar.vue'

// Estado reativo que controla se a tela é "desktop"
const isDesktop = ref(window.innerWidth >= 770)

// Função para atualizar o estado ao redimensionar
function handleResize() {
  isDesktop.value = window.innerWidth >= 770
}

// Registrar e remover o listener corretamente
onMounted(() => {
  window.addEventListener('resize', handleResize)
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', handleResize)
})
</script>

<template>
  <header class="main-header">
    <!-- Mostra o menu hambúrguer apenas em telas pequenas -->
    <MenuHamburguer v-if="!isDesktop" class="menu-hamburguer"/>

    <!-- Mostra a navbar apenas em telas grandes -->
    <NavBar v-if="isDesktop" class="menu-nav"/>

    <MainBanner/>
    <CardsContainer/>
  </header>
</template>

<style lang="scss">
.main-header {
  display: flex;
  flex-direction: column;
  align-items: stretch;
  background-color: #d4d4d4;
  text-align: center;
}
</style>
