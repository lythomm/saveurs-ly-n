<script setup lang="ts">
import { Phone, Mail, Facebook, Instagram } from "lucide-vue-next";
</script>

<template>
  <section id="contact" class="py-24 bg-[#0a0a0a] overflow-hidden">
    <div class="container mx-auto px-6">
      <div
        class="max-w-6xl mx-auto bg-white/5 border border-white/10 rounded-2xl overflow-hidden"
      >
        <div class="grid md:grid-cols-2">
          <div class="p-6 md:p-12 bg-gold/5 flex flex-col justify-center">
            <h2 class="text-4xl font-display mb-6 gold-gradient">
              Privatisation Foodtruck & Traiteur Asiatique
            </h2>
            <p class="text-gray-400 mb-8 leading-relaxed">
              Pour une commande spéciale, la privatisation de notre foodtruck
              pour un mariage à Lyon, ou faire appel à notre service de traiteur
              asiatique, n'hésitez pas à nous contacter.
            </p>

            <div class="space-y-6">
              <a href="tel:0650107030" class="flex items-center gap-4 group">
                <div
                  class="w-12 h-12 rounded-2xl bg-gold/10 flex items-center justify-center text-gold group-hover:bg-gold group-hover:text-black transition-all shrink-0"
                >
                  <Phone :size="20" />
                </div>
                <div>
                  <div class="text-xs text-gray-500 uppercase tracking-widest">
                    Téléphone
                  </div>
                  <div class="text-xl font-bold">06 50 10 70 30</div>
                </div>
              </a>

              <div class="flex items-center gap-4 group">
                <div
                  class="w-12 h-12 rounded-2xl bg-gold/10 flex items-center justify-center text-gold shrink-0"
                >
                  <Mail :size="20" />
                </div>
                <div>
                  <div class="text-xs text-gray-500 uppercase tracking-widest">
                    Email
                  </div>
                  <a
                    href="mailto:nouxiaxang.ly@gmail.com"
                    class="text-xl font-bold hover:text-gold transition-colors"
                  >
                    nouxiaxang.ly@gmail.com
                  </a>
                </div>
              </div>
            </div>

            <div class="mt-12 flex gap-4">
              <a
                href="#"
                class="w-10 h-10 rounded-2xl border border-white/10 flex items-center justify-center hover:bg-gold hover:text-black transition-all"
              >
                <Facebook :size="18" />
              </a>
              <a
                href="#"
                class="w-10 h-10 rounded-2xl border border-white/10 flex items-center justify-center hover:bg-gold hover:text-black transition-all"
              >
                <Instagram :size="18" />
              </a>
            </div>
          </div>

          <div class="relative min-h-[400px]">
            <img
              src="/catering_event.jpg"
              alt="Évènement professionnel et mariage traiteur asiatique foodtruck"
              class="absolute inset-0 w-full h-full object-cover"
            />
          </div>
        </div>
      </div>

    </div>
  </section>
</template>
