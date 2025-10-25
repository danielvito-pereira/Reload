<template>
  <div class="button-mobile">
    <RouterLink to="/" class="logo"><img src="/src/components/icons/icon logo.png" alt=""></RouterLink>
    <!-- Botão hambúrguer -->
    <button
      ref="buttonRef"
      class="hamburger-btn"
      :aria-expanded="isOpen.toString()"
      :aria-controls="menuId"
      @click="toggle"
      @keydown.space.prevent="toggle"
      @keydown.enter.prevent="toggle"
      :title="isOpen ? 'Fechar menu' : 'Abrir menu'"
    >
      <span class="sr-only">{{ isOpen ? 'Fechar menu' : 'Abrir menu' }}</span>
      <svg class="hamburger-icon" viewBox="0 0 24 24" width="24" height="24" aria-hidden="true">
        <rect :class="['line', {'line-top-open': isOpen}]" x="3" y="6" width="18" height="2" rx="1"></rect>
        <rect :class="['line', {'line-mid-open': isOpen}]" x="3" y="11" width="18" height="2" rx="1"></rect>
        <rect :class="['line', {'line-bot-open': isOpen}]" x="3" y="16" width="18" height="2" rx="1"></rect>
      </svg>
    </button>

    <!-- Backdrop -->
    <transition name="fade">
      <div
        v-if="isOpen"
        class="backdrop"
        @click="close"
        aria-hidden="true"
      />
    </transition>

    <!-- Drawer / Menu -->
    <transition name="slide">
      <nav
        v-if="isOpen"
        :id="menuId"
        ref="menuRef"
        class="drawer"
        role="menu"
        @keydown.esc.prevent="close"
      >
        <!-- Slot para conteúdo do menu -->
        <slot>
          <RouterLink to="/" class="logo"><img src="/src/components/icons/icon logo.png" alt=""></RouterLink>
          <!-- Conteúdo padrão (se usuário não passar slot) -->
          <ul class="menu-list">
            <RouterLink to="/">Home</RouterLink>
            <RouterLink to="/">Criação de Sites</RouterLink>
            <RouterLink to="/">Landing Pages</RouterLink>
            <RouterLink to="/about">Sobre</RouterLink>
            <RouterLink to="/">Quero um Orçamento</RouterLink>
          
          </ul>
      
        </slot>
        
      </nav>
    </transition>
  </div>
</template>

<script setup>
import { ref, watch, nextTick, onMounted, onBeforeUnmount } from 'vue'

/**
 * Props:
 * - modelValue (Boolean) -> controle externo via v-model
 * - placement (String) -> 'left' | 'right' (define animação)
 * - width (String) -> largura do drawer (ex: '80%', '300px')
 */
const props = defineProps({
  modelValue: { type: Boolean, default: false },
  placement: { type: String, default: 'left' },
  width: { type: String, default: '80%' },
  id: { type: String, default: null }
})
const emit = defineEmits(['update:modelValue', 'open', 'close'])

const isOpen = ref(props.modelValue)
const buttonRef = ref(null)
const menuRef = ref(null)
const menuId = props.id || `hamburger-menu-${Math.random().toString(36).slice(2,9)}`

// Sincroniza v-model
watch(() => props.modelValue, v => { isOpen.value = v })
watch(isOpen, value => {
  emit('update:modelValue', value)
  if (value) emit('open'); else emit('close')
  handleFocusOnToggle(value)
})

// Abre / fecha
function toggle() { isOpen.value = !isOpen.value }
function close() { isOpen.value = false }

// Quando abre, move foco para primeiro link; ao fechar, devolve foco ao botão
async function handleFocusOnToggle(open) {
  if (open) {
    await nextTick()
    // tenta focar o primeiro elemento focusable dentro do menu
    const focusable = menuRef.value?.querySelectorAll('a,button,input,[tabindex]:not([tabindex="-1"])')
    if (focusable && focusable.length) focusable[0].focus()
    // evita scroll no body
    document.body.style.overflow = 'hidden'
    // adiciona listener para trap de tab simples (melhora acessibilidade)
    document.addEventListener('focusin', keepFocusInside)
  } else {
    document.body.style.overflow = ''
    buttonRef.value?.focus()
    document.removeEventListener('focusin', keepFocusInside)
  }
}

// Implementação simples de focus-trap: se foco sair do menu, volta ao menu
function keepFocusInside(e) {
  if (!menuRef.value) return
  if (isOpen.value && !menuRef.value.contains(e.target) && e.target !== buttonRef.value) {
    // redireciona para o primeiro elemento dentro do menu
    const focusable = menuRef.value.querySelectorAll('a,button,input,[tabindex]:not([tabindex="-1"])')
    if (focusable && focusable.length) focusable[0].focus()
  }
}

// Limpeza ao desmontar
onBeforeUnmount(() => {
  document.body.style.overflow = ''
  document.removeEventListener('focusin', keepFocusInside)
})

// Ajusta classes de animação de acordo com placement
onMounted(() => {
  // aplica width dinamicamente via style (inline) no drawer
  if (menuRef.value) menuRef.value.style.setProperty('--drawer-width', props.width)
})
</script>

<style scoped>
.button-mobile{
  display: flex;
  flex-wrap: nowrap;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  width: 100%;
}
/* Reset sr-only */
.sr-only {
  position: absolute !important;
  width: 1px; height: 1px;
  padding: 0; margin: -1px;
  overflow: hidden; clip: rect(0,0,0,0); white-space: nowrap; border: 0;
}

/* Botão */
.hamburger-btn{
  display:inline-flex;
  align-items:center;
  justify-content:center;
  background:transparent;
  border:0;
  padding:8px;
  border-radius:8px;
  cursor:pointer;
}

/* Icon lines */
.hamburger-icon .line{
  fill: currentColor;
  transition: transform 0.28s ease, opacity 0.28s ease;
}

/* Transformações para estado aberto (cruz) */
.line-top-open {
  transform-origin: 12px 7px;
  transform: translateY(5px) rotate(45deg);
}
.line-mid-open {
  opacity: 0;
  transform: scaleX(0);
}
.line-bot-open {
  transform-origin: 12px 17px;
  transform: translateY(-5px) rotate(-45deg);
}

/* Backdrop */
.backdrop{
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.4);
  z-index: 40;
}

/* Drawer (menu lateral) */
.drawer{
  position: fixed;
  top: 0;
  bottom: 0;
  width: var(--drawer-width, 80%);
  text-align: justify;
  max-width: 420px;
  background: #D4D4D4;
  z-index: 50;
  padding: 1.25rem;
  box-shadow: 0 8px 32px rgba(0,0,0,0.12);
  overflow-y: auto;
  /* por padrão left, se user quiser right, pode sobrescrever com placement prop (ver JS) */
  left: 0;
}

/* Quando placement for right (o usuário pode sobrescrever via CSS caso queira) */
:root .drawer[placement="right"] {
  left: auto;
  right: 0;
}

/* Menu list básico */
.menu-list{
  list-style: none;
  padding: 0;
  margin: 0;
  display:flex;
  flex-direction:column;
  gap: 0.75rem;
}
.menu-list a{
  display:block;
  padding: 0.75rem 0.5rem;
  border-radius: 8px;
  text-decoration:none;
  font-weight:600;
}

/* Transições */
.fade-enter-active, .fade-leave-active { transition: opacity 200ms ease; }
.fade-enter-from, .fade-leave-to { opacity: 0; }
.fade-enter-to, .fade-leave-from { opacity: 1; }

.slide-enter-active, .slide-leave-active { transition: transform 260ms cubic-bezier(.2,.9,.2,1); }
.slide-enter-from { transform: translateX(-100%); }
.slide-enter-to { transform: translateX(0%); }
.slide-leave-from { transform: translateX(0%); }
.slide-leave-to { transform: translateX(-100%); }

/* Se quiser versão do drawer vindo da direita, no projeto coloque:
   .drawer.right { right: 0; left: auto; }
   .slide-enter-from { transform: translateX(100%); }
   .slide-leave-to { transform: translateX(100%); }
*/
</style>
