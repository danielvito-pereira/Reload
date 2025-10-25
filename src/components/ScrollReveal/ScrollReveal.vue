<!-- ScrollReveal.vue -->
<template>
  <div ref="reveal" :class="['scroll-reveal', { active: isActive }]">
    <slot />
  </div>
</template>

<script setup>
import { ref, onMounted, defineProps } from 'vue'

const props = defineProps({
  delay: {
    type: Number,
    default: 0 // milissegundos
  }
})

const isActive = ref(false)
const reveal = ref(null)

onMounted(() => {
  if (!reveal.value) return

  const observer = new IntersectionObserver(
    (entries, obs) => {
      const entry = entries[0]
      if (entry.isIntersecting) {
        // aplica delay antes de ativar
        setTimeout(() => {
          isActive.value = true
        }, props.delay)
        obs.unobserve(entry.target)
      }
    },
    { threshold: 0.2 }
  )

  observer.observe(reveal.value)
})
</script>

<style scoped lang="scss">
.scroll-reveal {
  opacity: 0;
  transform: translateY(40px);
  transition: all 0.8s ease-out;
}

.scroll-reveal.active {
  opacity: 1;
  transform: translateY(0);
}
</style>
