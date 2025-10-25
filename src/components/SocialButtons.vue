<template>
  <nav class="social-buttons">
    <h4 v-if="title">{{ title }}</h4>
    <ul>
      <SocialItems
        v-for="(item, i) in links"
        :key="i"
        :name="item.name"
        :icon="item.icon"
        :url="item.url"
      />
    </ul>
  </nav>
</template>

<script setup>
import SocialItems from './SocialItems.vue'

defineProps({
  title: String,
  links: { type: Array, default: () => [] },
})
</script>

<style scoped lang="scss">
.social-buttons {
  h4 {
    margin-bottom: 0.75rem;
    font-weight: 600;
  }

  ul {
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    gap: 0.5rem;
    list-style: none;
    padding: 0;
  }
}
</style>
