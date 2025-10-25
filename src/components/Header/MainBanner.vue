<template>
  <section class="reload-section">
    <crollReveal>
      <div class="text-content">
        <h1>Reload</h1>
        <p>
          Impacto digital autêntico,<br />
          presença online marcante<br />
          <!-- container que agrupa as duas palavras -->
          <span ref="highlight" class="highlight">
            <span class="word first">funcional e</span>
            <span class="word second">lucrativa.</span>
          </span>
        </p>
      </div>
    </crollReveal>
    <crollReveal :delay="200">   
      <div class="cta">
        <a href="#" class="contact-link">Entre em contato</a>
      </div>
    </crollReveal>
  </section>
</template>

<script setup>

import { ref, onMounted } from 'vue'
import crollReveal from '../ScrollReveal/ScrollReveal.vue'
const highlight = ref(null)

onMounted(() => {
  if (!highlight.value) return

  const observer = new IntersectionObserver(
    (entries, obs) => {
      const e = entries[0]
      if (e.isIntersecting) {
        // adiciona classe que aciona as transições/transformações
        highlight.value.classList.add('animate')
        obs.unobserve(highlight.value) // anima apenas uma vez
      }
    },
    { threshold: 0.35 }
  )

  observer.observe(highlight.value)
})
</script>

<style lang="scss" scoped>
.reload-section {
  display: grid;
  grid-template-columns: 1fr auto;
  align-items: center;
  padding: 5rem 1.5rem;
  gap: 2rem;
  text-align: left;

  @media (max-width: 768px) {
    grid-template-columns: 1fr;
    text-align: center;

    .cta {
      justify-self: center;
      font-size: 1.5rem;
    }
  }

  .text-content {
    h1 {
      font-size: 4.8rem;
      font-weight: 700;
      color: #1a1a1a;
      margin-bottom: 0.5rem;
    }

    p {
      font-size: 1.5rem;
      line-height: 1.6;
      color: #333;

      /* -- highlight container (mantém as duas palavras juntas) -- */
      .highlight {
        display: inline-block;
        /* relative para posicionar .second abaixo e deslocado */
        position: relative;
        margin-top: 6px;
        /* define comportamento inicial antes da animação */
        .word {
          display: block;
          transform-origin: left top;
        }

        /* primeira palavra (funcional) - fica na linha normal */
        .first {
          color: #e63946;
          font-weight: 700;
          transform: translateY(-40px) rotate(-2deg);
          opacity: 0;
          transition: transform 0.8s cubic-bezier(0.22, 1, 0.36, 1),
                      opacity 0.6s ease;
        }

        /* segunda palavra (lucrativa) - posicionada abaixo e inclinada */
        .second {
          color: #e63946;
          font-weight: 700;
          /* faz parecer que vem de cima e puxa para baixo + rotaciona */
          transform: translateY(-90px) translateX(6px) rotate(-12deg);
          opacity: 0;
          position: relative;
          left: 0;
          /* diminui o espaçamento vertical entre as palavras */
          margin-top: 0.05rem;
          transition:
            transform 0.9s cubic-bezier(0.2, 0.9, 0.2, 1),
            opacity 0.7s ease;
          /* ajusta tamanho levemente (opcional) para combinar com a imagem */
          font-size: 1.02em;
        }

        /* -- estado animado (após entrar na viewport) -- */
        &.animate {
          .first {
            transform: translateY(0) rotate(0deg);
            opacity: 1;
          }
          .second {
            /* posição final: abaixo da primeira, levemente deslocada e inclinada */
            transform: translateY(-3px) translateX(-1px) rotate(5deg);
            opacity: 1;
          }
        }
      } /* fim .highlight */
    } /* fim p */
  } /* fim .text-content */

  .cta {
    .contact-link {
      color: #e63946;
      text-decoration: none;
      font-weight: 500;
      border-bottom: 1px solid #e63946;
      padding-bottom: 2px;
      transition: color 0.2s, border-color 0.2s, background-color 0.3s ease;
      font-size: 1.5rem;
      &:hover {
        color: #b8232e;
        border-color: #b8232e;
      }
    }
  }
}

/* pequenos ajustes para telas muito pequenas: diminuir a rotação e deslocamento */
@media (max-width: 480px) {
  .reload-section {
    .text-content {
      p {
        .highlight {
          .second {
            transform: translateY(-70px) translateX(4px) rotate(5deg);
          }

          &.animate {
            .second {
              transform: translateY(-3px) translateX(-5px) rotate(5deg);
            }
          }
        }
      }
    }
  }
}
</style>
