<script setup lang="ts">
import { ref, onMounted, onUnmounted } from "vue";
import { Menu, X, Phone, Instagram, Facebook } from "lucide-vue-next";
import logoUrl from "../assets/logo.png";

const isScrolled = ref(false);
const isMenuOpen = ref(false);

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50;
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
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
  <!-- Main Header -->
  <header
    :class="[
      'fixed top-0 left-0 w-full z-[100] transition-all duration-700 ease-in-out',
      isScrolled || isMenuOpen
        ? 'py-3 bg-[#0a0a0a]/80 backdrop-blur-2xl border-b border-gold/10'
        : 'py-6 bg-transparent',
    ]"
  >
    <div
      class="container mx-auto px-6 max-w-7xl flex justify-between items-center"
    >
      <!-- Logo -->
      <a href="#home" class="relative group z-[110]" @click="closeMenu">
        <img
          :src="logoUrl"
          alt="LyN Logo"
          class="h-10 md:h-11 w-auto transition-transform duration-500 group-hover:scale-105"
        />
        <div
          class="absolute -inset-2 bg-gold/5 blur-xl rounded-full opacity-0 group-hover:opacity-100 transition-opacity"
        ></div>
      </a>

      <!-- Desktop Nav -->
      <nav class="hidden md:flex items-center gap-10">
        <div class="flex items-center gap-8">
          <a
            v-for="link in navLinks"
            :key="link.name"
            :href="link.href"
            class="text-[13px] font-medium text-white/70 hover:text-gold transition-all duration-300 tracking-[0.1em] uppercase relative group"
          >
            {{ link.name }}
            <span
              class="absolute -bottom-1 left-0 w-0 h-[1px] bg-gold transition-all duration-300 group-hover:w-full"
            ></span>
          </a>
        </div>

        <div class="h-6 w-[1px] bg-white/10"></div>

        <a
          href="tel:0650107030"
          class="flex items-center gap-3 bg-gold hover:bg-gold-light text-black px-6 py-2.5 rounded-full text-xs font-bold transition-all duration-300 transform hover:scale-105 hover:shadow-[0_0_20px_rgba(212,175,55,0.3)] group"
        >
          <Phone
            :size="14"
            class="group-hover:rotate-12 transition-transform"
          />
          06 50 10 70 30
        </a>
      </nav>

      <!-- Mobile Controls -->
      <div class="flex items-center gap-3 md:hidden z-[110]">
        <!-- Enhanced Mobile Phone Button -->
        <a
          href="tel:0650107030"
          class="relative flex items-center justify-center w-11 h-11 bg-gold text-black rounded-xl shadow-[0_4_15px_rgba(212,175,55,0.3)] transition-transform active:scale-95 group"
        >
          <Phone
            :size="20"
            fill="currentColor"
            class="group-hover:rotate-12 transition-transform"
          />
          <!-- Subtle ripple/pulse effect -->
          <span
            class="absolute inset-0 rounded-xl bg-gold opacity-20 pointer-events-none"
          ></span>
        </a>

        <!-- Menu Button -->
        <button
          @click="toggleMenu"
          class="relative w-11 h-11 flex items-center justify-center text-gold focus:outline-none bg-white/5 rounded-xl border border-white/10"
          aria-label="Menu"
        >
          <div class="relative w-6 h-5">
            <span
              :class="[
                'absolute block h-0.5 w-6 bg-current transition-all duration-300 ease-in-out',
                isMenuOpen ? 'rotate-45 top-2' : 'top-0',
              ]"
            ></span>
            <span
              :class="[
                'absolute block h-0.5 w-4 bg-current transition-all duration-300 ease-in-out top-2',
                isMenuOpen ? 'opacity-0 left-full' : 'opacity-100 left-0',
              ]"
            ></span>
            <span
              :class="[
                'absolute block h-0.5 bg-current transition-all duration-300 ease-in-out',
                isMenuOpen ? '-rotate-45 top-2 w-6' : 'top-4 w-5 right-0',
              ]"
            ></span>
          </div>
        </button>
      </div>
    </div>
  </header>

  <!-- Mobile Menu Overlay (Teleport to body to escape transform contexts) -->
  <Teleport to="body">
    <Transition
      enter-active-class="transition-opacity duration-500 ease-out"
      enter-from-class="opacity-0"
      enter-to-class="opacity-100"
      leave-active-class="transition-opacity duration-400 ease-in"
      leave-from-class="opacity-100"
      leave-to-class="opacity-0"
    >
      <div
        v-if="isMenuOpen"
        class="fixed inset-0 z-[90] bg-[#0a0a0a] flex flex-col pt-28 px-10 overflow-hidden"
      >
        <!-- Abstract background glows -->
        <div
          class="absolute top-[-10%] right-[-10%] w-[70%] h-[50%] bg-gold/5 blur-[120px] rounded-full pointer-events-none"
        ></div>
        <div
          class="absolute bottom-[-5%] left-[-5%] w-[60%] h-[40%] bg-gold/5 blur-[100px] rounded-full pointer-events-none"
        ></div>

        <!-- Navigation Links -->
        <div class="flex flex-col gap-4 relative z-10">
          <a
            v-for="(link, index) in navLinks"
            :key="link.name"
            :href="link.href"
            @click="closeMenu"
            v-motion
            :initial="{ opacity: 0, x: -30 }"
            :enter="{
              opacity: 1,
              x: 0,
              transition: {
                delay: 200 + index * 70,
                damping: 25,
                stiffness: 120,
              },
            }"
            class="text-4xl font-display font-light text-white hover:text-gold transition-colors inline-block"
          >
            <span class="text-gold/20 text-sm font-mono mr-4 italic"
              >0{{ index + 1 }}</span
            >
            {{ link.name }}
          </a>
        </div>

        <!-- Footer Mobile Menu -->
        <div
          class="mt-auto mb-16 space-y-8"
          v-motion
          :initial="{ opacity: 0, y: 30 }"
          :enter="{ opacity: 1, y: 0, transition: { delay: 600, damping: 25 } }"
        >
          <div class="h-px w-full bg-white/5"></div>

          <div class="relative group">
            <!-- Glassmorphism Card for Contact -->
            <div
              class="absolute -inset-4 bg-gold/5 blur-2xl rounded-[2rem] opacity-0 group-hover:opacity-100 transition-opacity duration-500"
            ></div>

            <div
              class="relative p-6 rounded-2xl bg-white/[0.03] border border-white/5 backdrop-blur-sm overflow-hidden"
            >
              <!-- Animated Shimmer Background -->
              <div
                class="absolute inset-0 bg-gradient-to-r from-transparent via-gold/5 to-transparent -translate-x-full group-hover:translate-x-full transition-transform duration-1000"
              ></div>

              <p
                class="text-gray-500 text-[10px] uppercase tracking-[0.3em] font-medium mb-4"
              >
                Réserver ou commander
              </p>

              <a href="tel:0650107030" class="flex flex-col gap-2">
                <span class="text-xs text-gold/60 font-medium"
                  >Directement par téléphone :</span
                >
                <div class="flex items-center gap-4">
                  <div
                    class="w-12 h-12 bg-gold rounded-xl flex items-center justify-center text-black shadow-lg shadow-gold/20 group-hover:rotate-6 transition-transform duration-300"
                  >
                    <Phone :size="24" fill="currentColor" />
                  </div>
                  <div class="flex flex-col">
                    <span
                      class="text-3xl font-bold text-white tracking-tight group-hover:text-gold transition-colors duration-300"
                      >06 50 10 70 30</span
                    >
                    <span class="text-[10px] text-gray-400 italic"
                      >Appel local • Lyon & Alentours</span
                    >
                  </div>
                </div>
              </a>
            </div>
          </div>

          <div class="flex gap-6">
            <a
              href="#"
              class="w-12 h-12 rounded-full border border-white/10 flex items-center justify-center text-white/50 hover:border-gold hover:text-gold transition-all duration-300"
            >
              <Instagram :size="22" />
            </a>
            <a
              href="#"
              class="w-12 h-12 rounded-full border border-white/10 flex items-center justify-center text-white/50 hover:border-gold hover:text-gold transition-all duration-300"
            >
              <Facebook :size="22" />
            </a>
          </div>
        </div>
      </div>
    </Transition>
  </Teleport>
</template>

<style scoped>
.font-display {
  font-family: var(--font-display, serif);
}

/* Ensure body doesn't jump when overflow hidden is applied if there's a scrollbar */
:global(body.overflow-hidden) {
  padding-right: var(--scrollbar-width, 0px);
}
</style>
