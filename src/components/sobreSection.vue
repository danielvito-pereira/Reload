<template>
  <BaseSection>
    <tituloH1>SOBRE</tituloH1> 
    <div class="about">
      <crollReveal>
        <Card  title="Reload Estudios" color="#252525" >
          A Reload Estudios nasceu com o propósito de transformar ideias em experiências visuais impactantes. Unimos criatividade e estratégia para construir identidades marcantes, designs funcionais e presenças digitais que conectam marcas ao seu público.Com anos de experiência em branding, design gráfico, mídias sociais e web design, ajudamos negócios a elevarem sua comunicação e se destacarem no universo digital.
        </Card>
      </crollReveal>
      <crollReveal>
        <div class="hero">
          <MainLogo class="mainLogo" size="15rem"/>
      </div>
     </crollReveal>
    </div>
  </BaseSection>
</template>
<script setup>
  import BaseSection from '@/components/Section/BaseSection.vue'
  import tituloH1 from '@/components/TituloH1.vue'
  import Card from '@/components/Cards/CardsP.vue'
  import MainLogo from '@/components/logo/MainLogo.vue'
  import crollReveal from '@/components/ScrollReveal/ScrollReveal.vue'
</script>
<style lang="scss" scoped>

  .about{
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;

    .hero{
      width: 100%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
     
  .logo {
    --logo-size: 25rem;

    img {
      width: var(--logo-size);
      height: auto;
      transition: transform 0.3s ease;
    }

    &:hover img {
      transform: scale(1.05);
    }
  }
      

    }  
  }

    @media (max-width: 770px){
      .about{
        display: flex;
        justify-content: space-between;
        align-items: center;
        flex-direction: column;
        gap:5rem;  
      }
    }
</style>
