<template>
  <div class="card">
    <h3 
    :style="{
      color: color,
      fontSize: size,
      textAlign: align,
      fontWeight: weight
    }" class="title">{{ title }}</h3>
    <p class="card-text">
      <slot />
    </p>
  </div>
</template>

<script setup>
  defineProps({
    title: {
      type: String,
      required: true
    },
    color: {
      type: String,
      default: '#e74c3c' // cor padrão
    },
    size: {
      type: String,
      default: '1.3rem'
    },
    align: {
      type: String,
      default: 'left'
    },
    weight: {
      type: String,
      default: '700'
    }
  })
</script>
<style lang="scss" scoped>
  .card {
    border: 1px solid #252525;
    border-radius: 10px;
    padding: 1.5rem;
    background-color: #fff;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    cursor: default;
    max-width: 24rem;
    &:hover {
      transform: translateY(-5px);
      box-shadow: 0 6px 20px rgba(0, 0, 0, 0.08);
    }

    .title {
      margin-bottom: 0.8rem;
    
    }

    .card-text {
      color: #333;
      font-size: 0.95rem;
      line-height: 1.4;
      text-align: left;
    }
  }
</style>