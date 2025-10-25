<template>
  <section class="carroselCards">
    <h2>{{ title }}</h2>
    <div class="carousel-wrapper">
      <div
        class="carousel-inner"
        :style="{ transform: `translateX(-${currentIndex * itemWidth}px)` }"
        ref="carouselInner"
      >
        <div
          class="carousel-item"
          v-for="(item, index) in items"
          :key="index"
        >
          <img :src="item.image" :alt="item.name" />
          <h3>{{ item.name }}</h3>
          <p>{{ item.area }}</p>
          <a :href="item.link" target="_blank">Veja o site</a>
        </div>
      </div>
    </div>
    <button class="prev" @click="prev">« Anterior</button>
    <button class="next" @click="next">Próximo »</button>
  </section>
</template>



<style  lang="scss" scoped>
.carroselCards {
  position: relative;
  overflow: hidden;
  margin: 2rem 0;

  h2 {
    text-align: center;
    margin-bottom: 1rem;
  }

  .carousel-wrapper {
    overflow: hidden;
  }

  .carousel-inner {
    display: flex;
    transition: transform 0.5s ease;
  }

  .carousel-item {
    min-width: 250px;
    margin-right: 16px;
    background: #f5f5f5;
    padding: 1rem;
    border-radius: 8px;
    text-align: center;

    img {
      max-width: 100%;
      border-radius: 4px;
      margin-bottom: 0.5rem;
    }

    h3 {
      margin: 0.5rem 0;
    }

    p {
      font-size: 0.9rem;
      color: #666;
    }

    a {
      display: inline-block;
      margin-top: 0.5rem;
      color: #007bff;
      text-decoration: none;
    }
  }

  button.prev,
  button.next {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    background: #007bff;
    color: #fff;
    border: none;
    padding: 0.5rem 1rem;
    cursor: pointer;
    border-radius: 4px;
  }

  button.prev {
    left: 0.5rem;
  }

  button.next {
    right: 0.5rem;
  }
}
</style>
