<template>
  <section class="pricing-section">
    <!-- Título da seção -->
    <h2 class="section-title">Escolha <span>Seu Plano</span></h2>

    <!-- Subtítulo explicativo -->
    <p class="section-subtitle">
      Whether you want to get organized, keep your personal life on track, or boost productivity.
    </p>

    <!--
      Container principal do carrossel.
      Eventos:
        @touchstart / @touchend -> para swipe em mobile
        @mouseenter / @mouseleave -> pausar/resumir autoplay em desktop com mouse
    -->
    <crollReveal>    
      <div
        class="carousel"
        @touchstart="handleTouchStart"
        @touchend="handleTouchEnd"
        @mouseenter="pauseAutoplay"
        @mouseleave="startAutoplay"
      >
        <!--
          Faixa (track) que será movida horizontalmente.
          :style="trackStyle" -> vinculamos um objeto JS (computed) que define transform.
        -->
        <div class="carousel-track" :style="trackStyle">
          <!--
            v-for: itera sobre "plans" (array no script) e cria um card por plano
            :key é obrigatório para performance e reconciliação pelo Vue
            :class adiciona a classe "active" quando currentIndex === index
          -->
          <div
            v-for="(plan, index) in plans"
            :key="index"
            class="card"
            :class="{ active: currentIndex === index }"
          >
            <h3 class="plan-name">{{ plan.name }}</h3>
            <p class="price">{{ plan.price }}</p>
            <p class="desc">{{ plan.desc }}</p>

            <!-- lista de features dentro do card -->
            <ul>
              <li v-for="(feature, i) in plan.features" :key="i">✔ {{ feature }}</li>
            </ul>

            <button class="btn">Get Started</button>
          </div>
        </div>

        <!-- indicadores (dots) - permitem ir direto para um slide -->
        <div class="indicators">
          <span
            v-for="(plan, index) in plans"
            :key="index"
            :class="{ active: currentIndex === index, animating: currentIndex === index && isAnimating }"
            @click="goToSlide(index)"
          >
            <span class="fill"></span>
          </span>
        </div>
      </div>
    </crollReveal>
  </section>
</template>


<script setup>
import { ref, computed, onMounted, onBeforeUnmount } from 'vue'
import crollReveal from '@/components/ScrollReveal/ScrollReveal.vue'
// 🔸 Dados estáticos dos planos
const plans = [
  {
    name: 'landing Page',
    price: '$500',
    desc: 'Captura de clientes',
    features: [
      'Vendas',
      'Clic-through',
      'Eventos',
      'Lançamentos',
    ],
  },
  {
    name: 'Squeeze Page',
    price: '$501.99',
    desc: 'captura de Leads',
    features: [
      'Captura de dados',
      'Vendas de produtos',
      'Reservas',
      'Lista de espera',
    ],
  },
  {
    name: 'Portfolio',
    price: '$249.99',
    desc: 'Presença digital',
    features: [
      'Coleção digital de trabalhos',
      'Estabelecer credibilidade',
      'Networking',
      'Criar uma marca pessoal',
    ],
  },
]

// 🔸 Estado reativo do carrossel
const currentIndex = ref(0)
const total = plans.length
let touchStartX = 0
let touchEndX = 0
let autoplayInterval = null
const autoplayDelay = 4000
const isAnimating = ref(false)

// 🔸 Controle de slides
const nextSlide = () => {
  currentIndex.value = (currentIndex.value + 1) % total
  restartIndicatorAnimation()
}

const prevSlide = () => {
  currentIndex.value = (currentIndex.value - 1 + total) % total
  restartIndicatorAnimation()
}

const goToSlide = (index) => {
  currentIndex.value = index
  restartIndicatorAnimation()
}

// 🔸 Detecção de gestos no mobile
const handleTouchStart = (e) => {
  touchStartX = e.changedTouches[0].screenX
}

const handleTouchEnd = (e) => {
  touchEndX = e.changedTouches[0].screenX
  handleGesture()
}

const handleGesture = () => {
  const deltaX = touchStartX - touchEndX
  if (Math.abs(deltaX) > 50) {
    deltaX > 0 ? nextSlide() : prevSlide()
  }
}

// 🔸 Controle do autoplay
const startAutoplay = () => {
  stopAutoplay()
  isAnimating.value = true
  autoplayInterval = setInterval(nextSlide, autoplayDelay)
}

const stopAutoplay = () => {
  clearInterval(autoplayInterval)
  autoplayInterval = null
}

const pauseAutoplay = () => {
  stopAutoplay()
  isAnimating.value = false
}

const restartIndicatorAnimation = () => {
  isAnimating.value = false
  void isAnimating.value
  setTimeout(() => (isAnimating.value = true), 50)
}

// 🔸 Ciclo de vida
onMounted(startAutoplay)
onBeforeUnmount(stopAutoplay)

// 🔸 Cálculo do deslocamento do carrossel
const trackStyle = computed(() => ({
  transform: `translateX(-${currentIndex.value * 100}%)`,
}))
</script>










<style scoped lang="scss">
.pricing-section {
  text-align: center;
  padding: 4rem 1rem;
  overflow: hidden;

  .section-title {
    font-size: 2rem;
    font-weight: 700;
    margin-bottom: 0.5rem;
    span {
      color: #ff2e00;
      position: relative;
    }
  }

  .section-subtitle {
    color: #555;
    max-width: 600px;
    margin: 0 auto 3rem;
  }

  .carousel {
    position: relative;
    /*
    overflow: hidden;
    */
    width: 100%;
    max-width: 1000px;
    margin: 0 auto;

    .carousel-track {
      display: flex;
      gap: 1rem;
      transition: transform 0.5s ease;
      width: 100%;
      flex-wrap: nowrap;
    }

    .card {
      flex: 0 0 100%;
      background: #f9f9f9;
      border-radius: 1rem;
      padding: 2rem;
      margin: 0 0.5rem;
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.142);
      text-align: left;
      transition: transform 0.3s ease;

      &.active {
        background: #ff2e00;
        color: #fff;
        transform: scale(1.05);
      }

      .plan-name {
        font-size: 1.5rem;
        font-weight: 600;
      }

      .price {
        font-size: 2rem;
        font-weight: 700;
        margin: 0.5rem 0;
      }

      .desc {
        margin-bottom: 1rem;
      }

      ul {
        list-style: none;
        padding: 0;
        margin-bottom: 1rem;
        li {
          margin: 0.3rem 0;
        }
      }

      .btn {
        background: #fff;
        color: #ff2e00;
        border: none;
        padding: 0.6rem 1.2rem ;
        border-radius: .5rem;
        cursor: pointer;
        font-weight: 600;
        transition: background 0.3s;

        &:hover {
          background: #e8f0fe;

        }
      }
    }

    .indicators {
      display: flex;
      justify-content: center;
      margin-top: 1.5rem;
      gap: 0.7rem;

      span {
        position: relative;
        width: 14px;
        height: 14px;
        border-radius: 50%;
        background: #ccc;
        cursor: pointer;
        overflow: hidden;

        &.active {
          background: #ff2e00;
        }

        .fill {
          position: absolute;
          top: 0;
          left: 0;
          width: 100%;
          height: 100%;
          background: rgba(255, 255, 255, 0.7);
          transform: scaleX(0);
          transform-origin: left;
        }

        &.animating .fill {
          animation: fillProgress linear forwards;
          animation-duration: 4s;
        }
      }
    }
  }
}

/* 🔹 MOBILE (até 767px) */
@media (max-width: 418px) {
  .pricing-section {

    .carousel{
      .card {
        flex: 0 0 91% !important;
      }
    }
  }


}
@media (max-width: 767px) {
  .pricing-section {
    background: #fff;
    padding: 2rem 1rem;
      .carousel {
      background: transparent;
        touch-action: pan-y;
    .carousel-track {
      display: flex;
      transition: transform 0.5s ease;
      width: 100%;
    }

    .card {
      flex: 0 0 93%;
      color: #fff;
      text-align: left;
      border-radius: 10px;
      padding: 1.8rem 1.5rem;
      box-shadow: none;

      .plan-name {
        font-weight: 600;
        margin-bottom: 0.5rem;
      }

      .price {
        font-size: 1.8rem;
        font-weight: 700;
        margin-bottom: 1rem;
        color: #fbbf24;
      }

      ul li {
        margin: 0.4rem 0;
      }

      .btn {
        display: block;
        width: 100%;
        border: none;
        border-radius: 8px;
        padding: 0.6rem 1rem;
        font-weight: 600;
        margin-top: 1rem;
      }
    }

    .indicators {
      margin-top: 1rem;
      span {
        width: 8px;
        height: 8px;
        background: #ccc;
      }
    }
  }
  }

  .section-title {
    font-size: 1.6rem;
    span {
      color: #fbbf24;
    }
  }

  .section-subtitle {
    color: #555;
    font-size: 0.9rem;
    max-width: 90%;
    margin: 0 auto 2rem;
  }


}



/* 🔹 DESKTOP (a partir de 768px) */
@media (min-width: 768px) {
  .carousel {
    overflow: visible !important;

    .carousel-track {
      transform: none !important;
      display: grid !important;
      grid-template-columns: repeat(3, 1fr);
      gap: 1rem;
    }

    .indicators {
      display: none;
    }

    .card {
      flex: 0 0 95%;
      flex: 1 !important;
    }
  }
}

@keyframes fillProgress {
  0% {
    transform: scaleX(0);
  }
  100% {
    transform: scaleX(1);
  }
}
</style>
