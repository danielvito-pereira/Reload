<template>
  <nav class="footer-social">
    <h4 v-if="title">{{ title }}</h4>
    <ul>
      <FooterSocialItem
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
import FooterSocialItem from './FooterSocialItem.vue'

defineProps({
  title: String,
  links: { type: Array, default: () => [] },
})
</script>

<style scoped lang="scss">
.footer-social {
  h4 {
    margin-bottom: 0.75rem;
    font-weight: 600;
  }

  ul {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    list-style: none;
    padding: 0;
  }
}
</style>
