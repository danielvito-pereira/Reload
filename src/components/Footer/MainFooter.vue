<template>
  <footer class="footer" :class="{ dark: isDark }">
    <div class="footer__container">
      <!-- Coluna 1: logo e descrição -->
      <div class="footer__brand">
        <FooterLogo />
        <p class="footer__slogan">
          Criando experiências digitais que conectam marcas e pessoas.
        </p>
      </div>
      <div class="teste">
        <!-- Coluna 2: navegação -->
        <FooterNav :links="navLinks" />

        <!-- Coluna 3: redes sociais -->
        <FooterSocial :links="socialLinks" title="Siga-nos" />
      </div>

    </div>

    <FooterCopyright />

    <!-- Botão para alternar tema
    <button class="footer__theme-toggle" @click="toggleTheme">
      <i :class="isDark ? 'fa-solid fa-sun' : 'fa-solid fa-moon'"></i>
    </button> -->
  </footer>
</template>

<script setup>
import { ref } from 'vue'
import FooterLogo from './FooterLogo.vue'
import FooterNav from './FooterNav.vue'
import FooterSocial from './FooterSocial.vue'
import FooterCopyright from './FooterCopyright.vue'

const isDark = ref(true)
/*
const toggleTheme = () => {
  isDark.value = !isDark.value
}
*/
// Links institucionais
const navLinks = [
  { name: 'Sobre', url: '/sobre' },
  { name: 'Serviços', url: '/servicos' },
  { name: 'Portfólio', url: '/portfolio' },
  { name: 'Contato', url: '/contato' },
]

// Redes sociais
const socialLinks = [
  { name: 'Instagram', icon: '/src/components/icons/instagram-icon.svg', url: 'https://instagram.com' },
  { name: 'Linkedin', icon: '/src/components/icons/linkedin-svgrepo-com.svg', url: 'https://behance.net' },
  { name: 'Orçamento', icon: '/src/components/icons/whatsapp-icon 1.svg', url: '/contato' },
]
</script>

<style scoped lang="scss">
.footer {
  color: #1e293b;
  padding: 3rem 1.5rem 2rem;
  position: relative;
  overflow: hidden;
  transition: background 0.4s, color 0.4s;

  &__container {
    max-width: 1200px;
    margin: 0 auto 2rem;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 2rem;
    @media screen and (max-width: 777px) {
      display: flex;
      flex-direction: column;
      flex-wrap:nowrap;
    }
    .teste{
      display: flex; 
      align-items: stretch;
      justify-content: space-around;
    }
  }

  &__brand {
    display: flex;
    flex-direction: column;
    gap: 0.75rem;

    .footer__slogan {
      font-size: 0.9rem;
      color: #64748b;
      max-width: 280px;
    }
  }

  /* Tema escuro
  &.dark {
    background: #0f172a;
    color: #f1f5f9;

    .footer__slogan {
      color: #94a3b8;
    }
  }

  /* Botão de alternância de tema 
  &__theme-toggle {
    position: absolute;
    right: 1rem;
    bottom: 1rem;
    background: transparent;
    border: none;
    color: inherit;
    cursor: pointer;
    font-size: 1.25rem;
    transition: transform 0.2s, color 0.3s;

    &:hover {
      transform: scale(1.1);
      color: #38bdf8;
    }
  } */
}
</style>
