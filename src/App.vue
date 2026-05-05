<script setup lang="ts">
import { ref, onMounted, onUnmounted, watch } from 'vue'
import Navbar from './components/Navbar.vue'
import Hero from './components/Hero.vue'
import About from './components/About.vue'
import Menu from './components/Menu.vue'
import Location from './components/Location.vue'
import FAQ from './components/FAQ.vue'
import Contact from './components/Contact.vue'
import Footer from './components/Footer.vue'
import Legal from './components/Legal.vue'
import { ArrowUp } from 'lucide-vue-next'

const showLegal = ref(false)
const showBackToTop = ref(false)

watch(showLegal, (isOpen) => {
  if (isOpen) {
    document.body.style.overflow = 'hidden'
  } else {
    document.body.style.overflow = ''
  }
})

const handleScroll = () => {
  showBackToTop.value = window.scrollY > 500
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}
</script>

<template>
  <div class="bg-[#0a0a0a] text-white selection:bg-gold selection:text-black overflow-x-hidden">
    <Navbar />
    <main>
      <Hero />
      <About />
      <Menu />
      <Location />
      <FAQ />
      <Contact />
    </main>
    <Footer @open-legal="showLegal = true" />
    <Legal :show="showLegal" @close="showLegal = false" />

    <!-- Back to top button -->
    <Transition
      enter-active-class="transition duration-300 ease-out"
      enter-from-class="opacity-0 translate-y-4"
      enter-to-class="opacity-100 translate-y-0"
      leave-active-class="transition duration-200 ease-in"
      leave-from-class="opacity-100 translate-y-0"
      leave-to-class="opacity-0 translate-y-4"
    >
      <button
        v-if="showBackToTop"
        @click="scrollToTop"
        class="fixed bottom-8 right-8 z-50 w-12 h-12 bg-gold text-black rounded-full shadow-lg shadow-gold/20 flex items-center justify-center hover:scale-110 active:scale-95 transition-all cursor-pointer"
        aria-label="Retour en haut"
      >
        <ArrowUp :size="24" />
      </button>
    </Transition>
  </div>
</template>

<style>
/* Any global transitions or adjustments */
html {
  scroll-behavior: smooth;
}

body {
  margin: 0;
  padding: 0;
  overflow-x: hidden;
}
</style>
