<template>
  <tituloH1>SERVIÇOS</tituloH1>
    <crollReveal :delay="250">
      <section class="cards">
      
        <Card title="Web Design">
          Mais que estética, experiências digitais envolventes e funcionais.
          Focamos na experiência do usuário para cativar e converter.
          Eleve sua presença digital conosco.
        </Card>

        <Card title="Criação de marca">
            Desenvolvemos marcas com propósito e identidade. Unimos estratégia e design para transmitir sua essência de forma autêntica e memorável.Construa uma marca forte e inspiradora ao nosso lado.
        </Card>

        <Card title="Social Media">
          Conectando marcas ao mundo digital. Nosso foco está na interação autêntica e no engajamento do público. Potencialize sua presença nas redes sociais conosco!
        </Card>
      </section>
    </crollReveal>

</template>

<script setup>
  import Card from '@/components/Cards/CardsP.vue'
  import tituloH1 from '@/components/TituloH1.vue'
  import crollReveal from '../ScrollReveal/ScrollReveal.vue'
</script>

<style scoped lang="scss">
.title{
  color: #FF2E00;
}
.cards {
  display: flex;
  flex-wrap: wrap;
  gap: 1.5rem;
  justify-content: center;
  padding: 1rem;
}
</style>