<script setup lang="ts">
import { Check } from "lucide-vue-next";
</script>

<template>
  <section id="about" class="py-24 bg-[#0a0a0a] overflow-hidden">
    <div class="container mx-auto px-6">
      <div class="max-w-6xl mx-auto">
        <div class="grid md:grid-cols-2 gap-16 items-center">
          <div class="order-2 md:order-1">
            <h2
              v-motion
              :initial="{ opacity: 0, y: 30, filter: 'blur(10px)' }"
              :visible-once="{
                opacity: 1,
                y: 0,
                filter: 'blur(0px)',
                transition: { duration: 800, ease: [0.22, 1, 0.36, 1] },
              }"
              class="text-4xl md:text-5xl font-display mb-8 leading-tight"
            >
              L'histoire d'une passion pour la
              <span class="gold-gradient italic"
                >cuisine asiatique authentique</span
              >
            </h2>

            <div class="space-y-6 text-gray-400 leading-relaxed">
              <p
                v-motion
                :initial="{ opacity: 0, y: 20 }"
                :visible-once="{
                  opacity: 1,
                  y: 0,
                  transition: { duration: 800, delay: 200, ease: 'easeOut' },
                }"
              >
                Saveurs de LyN est né d'une volonté simple : partager
                l'authenticité des saveurs asiatiques à travers des produits
                frais, faits maison et cuisinés avec passion. Notre
                <strong>foodtruck asiatique à Lyon</strong> parcourt les routes
                pour vous offrir une expérience culinaire unique.
              </p>
              <p
                v-motion
                :initial="{ opacity: 0, y: 20 }"
                :visible-once="{
                  opacity: 1,
                  y: 0,
                  transition: { duration: 800, delay: 300, ease: 'easeOut' },
                }"
              >
                Que ce soit sur le <strong>marché de Charly</strong> ou le
                <strong>marché de Millery</strong>, nous mettons un point
                d'honneur à préparer nos nems et bo bun à emporter selon des
                recettes traditionnelles. Chaque ingrédient est sélectionné pour
                sa qualité, garantissant des saveurs qui vous transportent
                instantanément.
              </p>
              <p
                v-motion
                :initial="{ opacity: 0, y: 20 }"
                :visible-once="{
                  opacity: 1,
                  y: 0,
                  transition: { duration: 800, delay: 400, ease: 'easeOut' },
                }"
              >
                Plus qu'un simple foodtruck, nous sommes également votre
                <strong>traiteur asiatique à Lyon</strong> pour tous vos
                événements. La
                <strong
                  >privatisation de notre foodtruck pour un mariage</strong
                >
                ou un événement professionnel est la solution idéale pour
                surprendre vos invités avec une cuisine raffinée et originale.
              </p>
            </div>

            <div class="mt-16 pt-8 border-t border-white/5">
              <div class="grid grid-cols-1 sm:grid-cols-2 gap-8">
                <div
                  v-motion
                  :initial="{ opacity: 0, x: -20 }"
                  :visible-once="{
                    opacity: 1,
                    x: 0,
                    transition: { duration: 800, delay: 600 },
                  }"
                  class="space-y-2"
                >
                  <div
                    class="text-gold font-bold uppercase tracking-wider text-xs"
                  >
                    Engagement
                  </div>
                  <h4 class="text-white font-medium">Produits de Qualité</h4>
                  <p class="text-gray-500 text-sm leading-relaxed">
                    Nous sélectionnons rigoureusement nos ingrédients pour
                    garantir fraîcheur et authenticité.
                  </p>
                </div>
                <div
                  v-motion
                  :initial="{ opacity: 0, x: -20 }"
                  :visible-once="{
                    opacity: 1,
                    x: 0,
                    transition: { duration: 800, delay: 800 },
                  }"
                  class="space-y-2"
                >
                  <div
                    class="text-gold font-bold uppercase tracking-wider text-xs"
                  >
                    Savoir-faire
                  </div>
                  <h4 class="text-white font-medium">Cuisine Artisanale</h4>
                  <p class="text-gray-500 text-sm leading-relaxed">
                    Toutes nos préparations sont réalisées à la main, dans le
                    respect des traditions.
                  </p>
                </div>
              </div>
            </div>
          </div>

          <div
            v-motion
            :initial="{ opacity: 0, scale: 0.9, rotate: 2 }"
            :visible-once="{
              opacity: 1,
              scale: 1,
              rotate: 0,
              transition: { duration: 1000, ease: [0.34, 1.56, 0.64, 1] },
            }"
            class="relative group order-1 md:order-2"
          >
            <div
              class="absolute -inset-4 bg-gold/10 blur-2xl rounded-full opacity-30 group-hover:opacity-50 transition-opacity"
            ></div>
            <div
              class="relative rounded-2xl overflow-hidden border border-white/10 shadow-2xl"
            >
              <img
                src="/about_us.jpg"
                alt="Saveurs de LyN - Privatisation Foodtruck mariage et évènement Lyon"
                class="w-full aspect-[4/5] object-cover hover:scale-105 transition-transform duration-700 brightness-110 contrast-[1.02]"
              />
              <!-- Sky Enhancer Overlay -->
              <div
                class="absolute inset-0 pointer-events-none bg-gradient-to-b from-blue-400/20 via-orange-300/10 to-transparent mix-blend-overlay"
              ></div>
              <div
                class="absolute inset-0 pointer-events-none bg-gradient-to-t from-[#0a0a0a]/40 to-transparent"
              ></div>
            </div>

            <!-- Floating Stats/Info -->
            <div
              v-motion
              :initial="{ opacity: 0, y: 40, scale: 0.8 }"
              :visible-once="{
                opacity: 1,
                y: 0,
                scale: 1,
                transition: {
                  duration: 800,
                  delay: 1000,
                  ease: [0.34, 1.56, 0.64, 1],
                },
              }"
              class="absolute -bottom-8 -left-8 bg-[#1a1a1a] border border-white/10 p-6 rounded-2xl shadow-xl hidden lg:block backdrop-blur-md"
            >
              <div class="space-y-3">
                <div class="flex items-center gap-3 text-sm font-medium">
                  <div
                    class="w-5 h-5 rounded-full bg-gold/20 flex items-center justify-center text-gold"
                  >
                    <Check :size="12" />
                  </div>
                  <span class="text-white">Produits Frais</span>
                </div>
                <div class="flex items-center gap-3 text-sm font-medium">
                  <div
                    class="w-5 h-5 rounded-full bg-gold/20 flex items-center justify-center text-gold"
                  >
                    <Check :size="12" />
                  </div>
                  <span class="text-white">Frais Maison</span>
                </div>
                <div class="flex items-center gap-3 text-sm font-medium">
                  <div
                    class="w-5 h-5 rounded-full bg-gold/20 flex items-center justify-center text-gold"
                  >
                    <Check :size="12" />
                  </div>
                  <span class="text-white">Recette Traditionnelle</span>
                </div>
                <div class="flex items-center gap-3 text-sm font-medium">
                  <div
                    class="w-5 h-5 rounded-full bg-gold/20 flex items-center justify-center text-gold"
                  >
                    <Check :size="12" />
                  </div>
                  <span class="text-white">Service Traiteur Lyon</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
