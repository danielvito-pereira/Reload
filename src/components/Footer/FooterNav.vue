<template>
  <nav class="footer-nav">
    <h4>Links úteis</h4>
    <ul>
      <li v-for="(link, i) in links" :key="i">
        <RouterLink :to="link.url">{{ link.name }}</RouterLink>
      </li>
    </ul>
  </nav>
</template>

<script setup>
defineProps({
  links: { type: Array, default: () => [] },
})
</script>

<style scoped lang="scss">
.footer-nav {
  h4 {
    margin-bottom: 0.75rem;
    font-weight: 600;
  }

  ul {
    list-style: none;
    padding: 0;
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
  }

  a {
    color: inherit;
    text-decoration: none;
    transition: color 0.2s;

    &:hover {
      color: #FF2E00;
    }
  }
}
</style>
