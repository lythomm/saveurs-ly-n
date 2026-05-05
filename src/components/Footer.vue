<script setup lang="ts">
import { Facebook, Instagram, Mail, Phone, MapPin } from "lucide-vue-next";
import logoUrl from "../assets/logo.png";

const emit = defineEmits(['open-legal']);

const navLinks = [
  { name: "Accueil", href: "#home" },
  { name: "À propos", href: "#about" },
  { name: "Menu", href: "#menu" },
  { name: "Où nous trouver", href: "#location" },
  { name: "Contact", href: "#contact" },
];
</script>

<template>
  <footer class="bg-[#050505] pt-20 pb-10 border-t border-white/5">
    <div class="container mx-auto px-6">
      <div class="max-w-6xl mx-auto">
        <div class="grid grid-cols-1 md:grid-cols-3 gap-12 mb-16">
          <!-- Brand Column -->
          <div class="flex flex-col gap-6">
            <a href="#home" class="inline-block">
              <img :src="logoUrl" alt="LyN Logo" class="h-12 w-auto" />
            </a>
            <p class="text-gray-400 leading-relaxed text-sm max-w-xs">
              Saveurs de LyN vous propose une expérience culinaire asiatique authentique au cœur de Lyon. Foodtruck, traiteur et évènementiel.
            </p>
            <div class="flex gap-4">
              <a
                href="#"
                class="w-10 h-10 rounded-full border border-white/10 flex items-center justify-center text-gray-400 hover:bg-gold hover:text-black hover:border-gold transition-all"
                aria-label="Facebook"
              >
                <Facebook :size="18" />
              </a>
              <a
                href="#"
                class="w-10 h-10 rounded-full border border-white/10 flex items-center justify-center text-gray-400 hover:bg-gold hover:text-black hover:border-gold transition-all"
                aria-label="Instagram"
              >
                <Instagram :size="18" />
              </a>
            </div>
          </div>

          <!-- Quick Links -->
          <div>
            <h3 class="text-white font-bold mb-6 uppercase tracking-widest text-xs">Navigation</h3>
            <ul class="flex flex-col gap-4">
              <li v-for="link in navLinks" :key="link.name">
                <a
                  :href="link.href"
                  class="text-gray-400 hover:text-gold transition-colors text-sm"
                >
                  {{ link.name }}
                </a>
              </li>
            </ul>
          </div>

          <!-- Contact Info -->
          <div>
            <h3 class="text-white font-bold mb-6 uppercase tracking-widest text-xs">Contact</h3>
            <ul class="flex flex-col gap-4">
              <li>
                <a href="tel:0650107030" class="flex items-center gap-3 text-gray-400 hover:text-gold transition-colors text-sm group">
                  <Phone :size="16" class="text-gold" />
                  06 50 10 70 30
                </a>
              </li>
              <li>
                <a href="mailto:nouxiaxang.ly@gmail.com" class="flex items-center gap-3 text-gray-400 hover:text-gold transition-colors text-sm group">
                  <Mail :size="16" class="text-gold" />
                  nouxiaxang.ly@gmail.com
                </a>
              </li>
              <li class="flex items-start gap-3 text-gray-400 text-sm">
                <MapPin :size="16" class="text-gold mt-0.5 shrink-0" />
                <span>Secteur Lyon et environs<br />Privatisation disponible</span>
              </li>
            </ul>
          </div>
        </div>

        <!-- Bottom Bar -->
        <div class="pt-8 border-t border-white/5 flex flex-col md:flex-row justify-between items-center gap-6 text-xs text-gray-500">
          <div>
            © {{ new Date().getFullYear() }} Saveurs de LyN. Tous droits réservés.
          </div>
          <div class="flex gap-8">
            <button @click="emit('open-legal')" class="hover:text-gold transition-colors cursor-pointer">Mentions Légales</button>
            <button @click="emit('open-legal')" class="hover:text-gold transition-colors cursor-pointer">Politique de Confidentialité</button>
          </div>
        </div>
      </div>
    </div>
  </footer>
</template>

<style scoped>
/* Any footer specific styles */
</style>
