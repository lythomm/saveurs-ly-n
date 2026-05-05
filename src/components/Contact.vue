<script setup lang="ts">
import { Phone, Mail, Facebook, Instagram } from "lucide-vue-next";
</script>

<template>
  <section id="contact" class="py-24 bg-[#0a0a0a] overflow-hidden">
    <div class="container mx-auto px-6">
      <div
        v-motion
        :initial="{ opacity: 0, y: 50, scale: 0.98 }"
        :visible-once="{ 
          opacity: 1, 
          y: 0, 
          scale: 1,
          transition: { duration: 1000, ease: [0.22, 1, 0.36, 1] } 
        }"
        class="max-w-6xl mx-auto bg-white/5 border border-white/10 rounded-3xl overflow-hidden shadow-2xl backdrop-blur-sm"
      >
        <div class="grid md:grid-cols-2">
          <div class="p-8 md:p-16 bg-gold/5 flex flex-col justify-center relative overflow-hidden">
            <!-- Background Decoration -->
            <div class="absolute -top-24 -left-24 w-64 h-64 bg-gold/5 rounded-full blur-3xl"></div>
            
            <h2 
              v-motion
              :initial="{ opacity: 0, x: -30, filter: 'blur(10px)' }"
              :visible-once="{ 
                opacity: 1, 
                x: 0, 
                filter: 'blur(0px)',
                transition: { delay: 300, duration: 800, ease: 'easeOut' } 
              }"
              class="text-4xl md:text-5xl font-display mb-8 gold-gradient relative z-10"
            >
              Privatisation Foodtruck & Traiteur Asiatique
            </h2>
            <p 
              v-motion
              :initial="{ opacity: 0, y: 20 }"
              :visible-once="{ 
                opacity: 1, 
                y: 0, 
                transition: { delay: 500, duration: 800, ease: 'easeOut' } 
              }"
              class="text-gray-400 mb-10 leading-relaxed text-lg relative z-10"
            >
              Pour une commande spéciale, la privatisation de notre foodtruck
              pour un mariage à Lyon, ou faire appel à notre service de traiteur
              asiatique, n'hésitez pas à nous contacter.
            </p>

            <div class="space-y-8 relative z-10">
              <a 
                v-motion
                :initial="{ opacity: 0, x: -20 }"
                :visible-once="{ 
                  opacity: 1, 
                  x: 0, 
                  transition: { delay: 700, duration: 600, ease: 'backOut' } 
                }"
                href="tel:0650107030" 
                class="flex items-center gap-5 group"
              >
                <div
                  class="w-14 h-14 rounded-2xl bg-gold/10 flex items-center justify-center text-gold group-hover:bg-gold group-hover:text-black group-hover:scale-110 group-hover:rotate-6 transition-all duration-500 shrink-0 shadow-[0_0_20px_rgba(212,175,55,0)] group-hover:shadow-[0_0_20px_rgba(212,175,55,0.3)]"
                >
                  <Phone :size="24" />
                </div>
                <div>
                  <div class="text-xs text-gray-500 uppercase tracking-[0.2em] mb-1">
                    Téléphone
                  </div>
                  <div class="text-2xl font-bold group-hover:text-gold transition-colors duration-300">06 50 10 70 30</div>
                </div>
              </a>

              <div 
                v-motion
                :initial="{ opacity: 0, x: -20 }"
                :visible-once="{ 
                  opacity: 1, 
                  x: 0, 
                  transition: { delay: 850, duration: 600, ease: 'backOut' } 
                }"
                class="flex items-center gap-5 group"
              >
                <div
                  class="w-14 h-14 rounded-2xl bg-gold/10 flex items-center justify-center text-gold shrink-0 transition-all duration-500 group-hover:bg-gold/20 group-hover:scale-110 group-hover:-rotate-6"
                >
                  <Mail :size="24" />
                </div>
                <div>
                  <div class="text-xs text-gray-500 uppercase tracking-[0.2em] mb-1">
                    Email
                  </div>
                  <a
                    href="mailto:nouxiaxang.ly@gmail.com"
                    class="text-xl md:text-2xl font-bold hover:text-gold transition-colors duration-300 break-all md:break-normal"
                  >
                    nouxiaxang.ly@gmail.com
                  </a>
                </div>
              </div>
            </div>

            <div class="mt-16 flex gap-6 relative z-10">
              <a
                v-motion
                :initial="{ opacity: 0, scale: 0.5 }"
                :visible-once="{ 
                  opacity: 1, 
                  scale: 1, 
                  transition: { delay: 1100, duration: 500, ease: 'backOut' } 
                }"
                href="#"
                class="w-12 h-12 rounded-2xl border border-white/10 flex items-center justify-center hover:bg-gold hover:text-black hover:border-gold hover:scale-110 hover:-translate-y-1 transition-all duration-500 group"
              >
                <Facebook :size="20" class="group-hover:animate-pulse" />
              </a>
              <a
                v-motion
                :initial="{ opacity: 0, scale: 0.5 }"
                :visible-once="{ 
                  opacity: 1, 
                  scale: 1, 
                  transition: { delay: 1200, duration: 500, ease: 'backOut' } 
                }"
                href="#"
                class="w-12 h-12 rounded-2xl border border-white/10 flex items-center justify-center hover:bg-gold hover:text-black hover:border-gold hover:scale-110 hover:-translate-y-1 transition-all duration-500 group"
              >
                <Instagram :size="20" class="group-hover:animate-pulse" />
              </a>
            </div>
          </div>

          <div 
            v-motion
            :initial="{ opacity: 0, scale: 1.1, filter: 'blur(20px)' }"
            :visible-once="{ 
              opacity: 1, 
              scale: 1, 
              filter: 'blur(0px)',
              transition: { delay: 400, duration: 1500, ease: [0.22, 1, 0.36, 1] } 
            }"
            class="relative min-h-[500px] overflow-hidden group"
          >
            <img
              src="/catering_event.jpg"
              alt="Évènement professionnel et mariage traiteur asiatique foodtruck"
              class="absolute inset-0 w-full h-full object-cover transition-transform duration-[3000ms] group-hover:scale-110"
            />
            <div class="absolute inset-0 bg-gradient-to-t from-black/60 to-transparent md:bg-gradient-to-l opacity-60 group-hover:opacity-40 transition-opacity duration-1000"></div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
