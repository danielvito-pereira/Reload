<template>
  <div class="logo">
    <RouterLink to="/">
      <img
        :src="src"
        :alt="alt"
        :style="{ width: size, height: 'auto' }"/>
    </RouterLink>
  </div>
</template>


<script setup>
  defineProps({
    src: {
      type: String,
      default: '/src/components/icons/icon_logo.svg'
    },
    alt: {
      type: String,
      default: 'Logo da empresa'
    },
    size: {
      type: String,
      default: '2.5rem' 
    }
  })
</script>


<style scoped lang="scss">
.logo {
  img {
    height: auto;
    transition: transform 0.3s ease;
  }

  &:hover img {
    transform: scale(1.05);
  }
}
</style>
