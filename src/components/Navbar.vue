<script setup lang="ts">
import { ref, onMounted } from "vue";
import { Menu, X, Phone } from "lucide-vue-next";
import logoUrl from "../assets/logo.png";

const isScrolled = ref(false);
const isMenuOpen = ref(false);

onMounted(() => {
  window.addEventListener("scroll", () => {
    isScrolled.value = window.scrollY > 50;
  });
});

const navLinks = [
  { name: "Accueil", href: "#home" },
  { name: "À propos", href: "#about" },
  { name: "Menu", href: "#menu" },
  { name: "Où nous trouver", href: "#location" },
  { name: "Contact", href: "#contact" },
];

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
  if (isMenuOpen.value) {
    document.body.style.overflow = "hidden";
  } else {
    document.body.style.overflow = "";
  }
};

const closeMenu = () => {
  isMenuOpen.value = false;
  document.body.style.overflow = "";
};
</script>

<template>
  <nav
    :class="[
      'fixed w-full z-50 transition-all duration-500 flex justify-center',
      isScrolled
        ? 'bg-[#0a0a0a]/90 backdrop-blur-md border-b border-gold/20 py-3'
        : 'bg-transparent py-4',
    ]"
  >
    <div
      class="container mx-auto px-6 md:px-0 max-w-6xl flex justify-between items-center w-full"
    >
      <!-- Logo -->
      <a href="#home" class="flex items-center gap-2 z-50" @click="closeMenu">
        <img :src="logoUrl" alt="LyN Logo" class="h-10 md:h-12 w-auto" />
      </a>

      <!-- Desktop Nav -->
      <div class="hidden md:flex items-center gap-8">
        <a
          v-for="link in navLinks"
          :key="link.name"
          :href="link.href"
          class="text-sm font-medium hover:text-gold transition-colors tracking-wide"
        >
          {{ link.name }}
        </a>
        <a
          href="tel:0650107030"
          class="bg-gold hover:bg-gold-light text-black px-6 py-2.5 rounded-full text-sm font-bold transition-all transform hover:scale-105 flex items-center gap-2 shadow-lg shadow-gold/20"
        >
          <Phone :size="16" />
          06 50 10 70 30
        </a>
      </div>

      <!-- Mobile Menu Toggle -->
      <button
        class="md:hidden text-gold z-50 p-2"
        @click="toggleMenu"
        aria-label="Toggle Menu"
      >
        <Menu v-if="!isMenuOpen" :size="28" />
        <X v-else :size="28" />
      </button>
    </div>

    <!-- Mobile Nav Overlay -->
    <Transition
      enter-active-class="transition duration-300 ease-out"
      enter-from-class="opacity-0 translate-y-4"
      enter-to-class="opacity-100 translate-y-0"
      leave-active-class="transition duration-200 ease-in"
      leave-from-class="opacity-100 translate-y-0"
      leave-to-class="opacity-0 translate-y-4"
    >
      <div
        v-if="isMenuOpen"
        class="fixed inset-0 bg-[#0a0a0a]/98 z-40 flex flex-col items-center justify-center gap-8 md:hidden p-8"
      >
        <div class="flex flex-col items-center gap-6">
          <a
            v-for="link in navLinks"
            :key="link.name"
            :href="link.href"
            class="text-3xl font-display font-light hover:text-gold transition-colors"
            @click="closeMenu"
          >
            {{ link.name }}
          </a>

          <div class="w-12 h-px bg-gold/30 my-4"></div>

          <a
            href="tel:0650107030"
            class="flex flex-col items-center gap-2 group"
            @click="closeMenu"
          >
            <span class="text-xs text-gray-500 uppercase tracking-widest"
              >Contactez-nous</span
            >
            <span
              class="text-2xl font-bold text-gold group-hover:text-gold-light transition-colors"
            >
              06 50 10 70 30
            </span>
          </a>

          <a
            href="tel:0650107030"
            class="mt-4 bg-gold text-black px-10 py-4 rounded-full text-lg font-bold tracking-widest uppercase hover:bg-gold-light transition-all flex items-center gap-3"
            @click="closeMenu"
          >
            <Phone :size="20" />
            Appeler
          </a>
        </div>
      </div>
    </Transition>
  </nav>
</template>

<style scoped>
.font-display {
  font-family: var(--font-display);
}
</style>
