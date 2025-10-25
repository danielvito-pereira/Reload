<template>
  <li class="social-item">
    <a
      :href="url"
      :target="isExternal ? '_blank' : '_self'"
      rel="noopener noreferrer"
    >
      <img :src="resolvedIcon" :alt="name" />
      <span>{{ name }}</span>
    </a>
  </li>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  name: String,
  icon: String,
  url: String,
})

const isExternal = computed(() => props.url?.startsWith('http'))

// garante que o ícone carregue mesmo em build
const resolvedIcon = computed(() => new URL(props.icon, import.meta.url).href)
</script>

<style scoped lang="scss">
.social-item {
  a {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    color: inherit;
    text-decoration: none;
    transition: color 0.3s, transform 0.2s;

    &:hover {
      color: #FF2E00;
      transform: scale(1.05);
    }

    img {
      width: 22px;
      height: 22px;
      filter: brightness(0.9);
      transition: filter 0.3s;
    }

    &:hover img {
      filter: brightness(1.2);
    }
  }
}
</style>
