<template>
  <div class="wrapper">
    <RouterLink to="/">
      <MainLogo />
    </RouterLink>

    <nav class="navBar">
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="">Criação de Sites</RouterLink>
      <RouterLink to="">Landing Pages</RouterLink>
      <RouterLink to="">Sobre</RouterLink>
      <RouterLink to="">Quero um Orçamento</RouterLink>
    </nav>

    <SocialButtons :links="socialLinks" />
  </div>

  <RouterView />
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import { RouterLink, RouterView } from 'vue-router'
import MainLogo from '../logo/MainLogo.vue'
import SocialButtons from '../SocialButtons.vue'

// Links das redes sociais
const socialLinks = [
  { icon: '/src/components/icons/instagram-icon.svg', url: 'https://instagram.com' },
  { icon: '/src/components/icons/linkedin-svgrepo-com.svg', url: 'https://behance.net' },
  { icon: '/src/components/icons/whatsapp-icon 1.svg', url: '/contato' }
]

// Controle responsivo do tamanho da fonte
const fontSize = ref('0.75rem')

function updateFontSize() {
  const width = window.innerWidth

  if (width < 480) {
    fontSize.value = '0.7rem'
  } else if (width < 770) {
    fontSize.value = '0.8rem'
  } else if (width < 1024) {
    fontSize.value = '0.9rem'
  } else {
    fontSize.value = '1rem'
  }
}

onMounted(() => {
  updateFontSize()
  window.addEventListener('resize', updateFontSize)
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', updateFontSize)
})
</script>

<style scoped lang="scss">
.wrapper {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  width: 100%;
  gap: 1rem;

  .navBar {
    display: flex;
    gap: 1rem;
    justify-content: center;
    align-items: center;
    flex-wrap: nowrap;
  }

  a {
    text-decoration: none;
    color: var(--color-text, #000);
    transition: color 0.3s ease, transform 0.2s ease;
    font-weight: 500;
    font-size: v-bind(fontSize); // <-- Usa o tamanho reativo da fonte

    &:hover {
      color:  #FF2E00;
      transform: scale(1.05);
    }
/*
    &.router-link-exact-active {
      color:  #FF2E00;
      font-weight: 600;
    }*/
  }
}
</style>
