<script setup lang="ts">
import logoUrl from "../assets/logo.png";
import heroBgUrl from "../assets/hero-bg.png";
import { onMounted } from "vue";

onMounted(() => {
  const schema = {
    "@context": "https://schema.org",
    "@type": "FoodEstablishment",
    name: "Saveurs de LyN",
    image: "https://saveurs-lyn.fr/logo.png",
    "@id": "",
    url: "https://saveurs-lyn.fr",
    telephone: "0650107030",
    menu: "https://saveurs-lyn.fr/#menu",
    servesCuisine: "Asiatique",
    description:
      "Foodtruck asiatique à Lyon et traiteur. Nems, bo bun à emporter sur les marchés de Charly et Millery. Privatisation de foodtruck pour mariage à Lyon.",
    address: {
      "@type": "PostalAddress",
      addressLocality: "Lyon",
      addressRegion: "Auvergne-Rhône-Alpes",
      addressCountry: "FR",
    },
  };
  const script = document.createElement("script");
  script.setAttribute("type", "application/ld+json");
  script.textContent = JSON.stringify(schema);
  document.head.appendChild(script);
});
</script>

<template>
  <section
    id="home"
    class="relative min-h-screen flex items-center justify-center overflow-hidden"
  >
    <!-- Background Image & Overlay -->
    <div
      class="absolute inset-0 z-0 bg-cover bg-center bg-no-repeat opacity-40"
      :style="{ backgroundImage: `url(${heroBgUrl})` }"
    ></div>
    <div
      class="absolute inset-0 bg-gradient-to-b from-transparent via-[#0a0a0a]/50 to-[#0a0a0a] z-0"
    ></div>

    <div class="container mx-auto px-6 relative z-10">
      <div class="max-w-6xl mx-auto flex flex-col items-center text-center">
        <div
          v-motion
          :initial="{ opacity: 0, scale: 0.8, y: 50 }"
          :enter="{
            opacity: 1,
            scale: 1,
            y: 0,
            transition: { duration: 1000 },
          }"
          class="mb-8"
        >
          <img
            :src="logoUrl"
            alt="Saveurs de LyN Logo"
            class="w-52 drop-shadow-[0_0_30px_rgba(212,175,55,0.3)]"
          />
        </div>

        <h1
          v-motion
          :initial="{ opacity: 0, y: 20 }"
          :enter="{
            opacity: 1,
            y: 0,
            transition: { delay: 400, duration: 800 },
          }"
          class="text-4xl md:text-6xl font-display font-light mb-4 tracking-wider"
        >
          L'excellence du
          <span class="gold-gradient italic font-normal"
            >Foodtruck Asiatique à Lyon</span
          >
        </h1>

        <p
          v-motion
          :initial="{ opacity: 0, y: 20 }"
          :enter="{
            opacity: 1,
            y: 0,
            transition: { delay: 600, duration: 800 },
          }"
          class="text-lg md:text-xl text-gray-400 max-w-2xl mb-12 font-light"
        >
          Découvrez Saveurs de LyN, votre traiteur asiatique sur Lyon et ses
          alentours. Dégustez nos nems et bo bun à emporter faits maison, ou
          optez pour la privatisation de notre foodtruck pour votre mariage ou
          événement professionnel.
        </p>

        <div
          v-motion
          :initial="{ opacity: 0, y: 20 }"
          :enter="{
            opacity: 1,
            y: 0,
            transition: { delay: 800, duration: 800 },
          }"
          class="flex flex-col sm:flex-row gap-4"
        >
          <a
            href="#menu"
            class="gold-border px-10 py-4 rounded-2xl text-gold font-bold hover:scale-105 transition-transform"
          >
            DÉCOUVRIR LE MENU
          </a>
          <a
            href="#contact"
            class="bg-white/5 border border-white/10 px-10 py-4 rounded-2xl text-white font-medium hover:bg-white/10 transition-all"
          >
            NOUS CONTACTER
          </a>
        </div>
      </div>
    </div>
  </section>
</template>
