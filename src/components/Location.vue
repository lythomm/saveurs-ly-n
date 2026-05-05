<script setup lang="ts">
import { ref, onMounted, onUnmounted, watch } from "vue";
import { MapPin, Calendar, Clock } from "lucide-vue-next";
import L from "leaflet";
import "leaflet/dist/leaflet.css";

const locations = [
  {
    day: "Samedi Matin",
    name: "Marché de Millery",
    location: "Place du Marché, 69390 Millery",
    time: "07:30 - 12:30",
    coords: [45.632731854265586, 4.782253618343297] as [number, number],
  },
  {
    day: "Dimanche Matin",
    name: "Marché de Charly",
    location: "Place de la Mairie, 69390 Charly",
    time: "08:00 - 12:00",
    coords: [45.64928281433973, 4.794773608966779] as [number, number],
  },
];

const selectedIdx = ref(0);
const mapContainer = ref<HTMLElement | null>(null);
let map: L.Map | null = null;
let marker: L.Marker | null = null;

const initMap = () => {
  if (!mapContainer.value) return;

  const initialCoords = locations[selectedIdx.value].coords;
  map = L.map(mapContainer.value, {
    zoomControl: false, // We'll position it better via CSS or keep it hidden for premium feel
  }).setView(initialCoords, 15);

  L.tileLayer(
    "https://{s}.basemaps.cartocdn.com/rastertiles/voyager/{z}/{x}/{y}{r}.png",
    {
      attribution:
        '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors &copy; <a href="https://carto.com/attributions">CARTO</a>',
      subdomains: "abcd",
      maxZoom: 20,
    },
  ).addTo(map);

  // Custom Gold Marker with Pulse
  const goldIcon = L.divIcon({
    className: "custom-div-icon",
    html: `
      <div class="relative flex items-center justify-center">
        <div class="absolute w-8 h-8 bg-gold rounded-full animate-slow-pulse"></div>
        <div class="relative w-4 h-4 bg-gold rounded-full border-2 border-white shadow-[0_0_15px_rgba(212,175,55,0.8)]"></div>
      </div>
    `,
    iconSize: [32, 32],
    iconAnchor: [16, 16],
  });

  marker = L.marker(initialCoords, { icon: goldIcon }).addTo(map);

  // Re-add zoom control to the right
  L.control.zoom({ position: "topright" }).addTo(map);
};

const selectLocation = (idx: number) => {
  selectedIdx.value = idx;
  if (map && marker) {
    const coords = locations[idx].coords;
    map.flyTo(coords, 16, {
      duration: 1.5,
      easeLinearity: 0.25,
    });
    marker.setLatLng(coords);
  }
};

onMounted(() => {
  initMap();
});

onUnmounted(() => {
  if (map) {
    map.remove();
  }
});
</script>

<template>
  <section id="location" class="py-24 relative bg-[#0a0a0a] overflow-hidden">
    <div class="container mx-auto px-6">
      <div class="max-w-6xl mx-auto">
        <div class="grid lg:grid-cols-2 gap-16">
          <div>
            <h2 
              v-motion
              :initial="{ opacity: 0, y: 30, filter: 'blur(10px)' }"
              :visible-once="{ 
                opacity: 1, 
                y: 0, 
                filter: 'blur(0px)',
                transition: { duration: 800, ease: [0.22, 1, 0.36, 1] } 
              }"
              class="text-3xl md:text-5xl font-display mb-8 gold-gradient"
            >
              Où trouver notre Foodtruck Asiatique ?
            </h2>
            
            <div class="mb-12 space-y-4">
              <p 
                v-motion
                :initial="{ opacity: 0, y: 20 }"
                :visible-once="{ 
                  opacity: 1, 
                  y: 0, 
                  transition: { delay: 200, duration: 800, ease: 'easeOut' } 
                }"
                class="text-lg font-light leading-relaxed"
              >
                Retrouvez les Saveurs de LyN chaque week-end sur les marchés de l'Ouest Lyonnais. Nous sommes fiers d'être votre foodtruck au marché de Millery et votre foodtruck au marché de Charly.
              </p>
              <p 
                v-motion
                :initial="{ opacity: 0, y: 20 }"
                :visible-once="{ 
                  opacity: 1, 
                  y: 0, 
                  transition: { delay: 350, duration: 800, ease: 'easeOut' } 
                }"
                class="text-gray-400"
              >
                Commandez vos nems et bo bun à emporter directement sur place. Cliquez sur un lieu pour le voir sur la carte.
              </p>
            </div>

            <div class="grid gap-6">
              <button
                v-for="(slot, idx) in locations"
                :key="slot.name"
                @click="selectLocation(idx)"
                v-motion
                :initial="{ opacity: 0, x: -30 }"
                :visible-once="{ 
                  opacity: 1, 
                  x: 0, 
                  transition: { 
                    delay: 500 + (idx * 150), 
                    duration: 800, 
                    ease: [0.34, 1.56, 0.64, 1] 
                  } 
                }"
                class="w-full text-left bg-white/5 border p-6 rounded-2xl transition-all duration-500 group relative overflow-hidden cursor-pointer"
                :class="
                  selectedIdx === idx
                    ? 'border-gold bg-gold/5 shadow-[0_0_30px_rgba(212,175,55,0.1)]'
                    : 'border-white/10 hover:border-gold/30 hover:bg-white/8'
                "
              >
                <div
                  v-if="selectedIdx === idx"
                  class="absolute left-0 top-0 bottom-0 w-1 bg-gold shadow-[0_0_15px_#d4af37]"
                ></div>
                <div class="flex items-center justify-between gap-4 w-full relative z-10">
                  <div class="transition-transform duration-500 group-hover:translate-x-1">
                    <h4 class="text-lg font-bold text-white mb-1">
                      {{ slot.day }}
                    </h4>
                    <div class="flex items-center gap-2 text-gold-light group-hover:text-gold transition-colors duration-300">
                      <MapPin :size="16" />
                      <span>{{ slot.name }}</span>
                    </div>
                  </div>
                  <div
                    class="flex items-center gap-2 text-gray-400 text-sm bg-white/5 px-4 py-2 rounded-xl border border-white/5 transition-all duration-300 group-hover:bg-gold/10 group-hover:border-gold/20"
                  >
                    <Clock :size="14" class="text-gold" />
                    <span class="font-medium group-hover:text-white transition-colors">{{ slot.time }}</span>
                  </div>
                </div>
              </button>
            </div>
          </div>

          <div
            v-motion
            :initial="{ opacity: 0, scale: 0.95, filter: 'grayscale(1)' }"
            :visible-once="{ 
              opacity: 1, 
              scale: 1, 
              filter: 'grayscale(0)',
              transition: { delay: 400, duration: 1200, ease: [0.22, 1, 0.36, 1] } 
            }"
            class="relative aspect-square md:aspect-video lg:aspect-square rounded-2xl overflow-hidden border border-gold/20 z-0 group"
          >
            <div
              ref="mapContainer"
              class="absolute inset-0 h-full w-full transition-transform duration-1000 group-hover:scale-105"
            ></div>

            <!-- Overlay Info -->
            <div
              class="absolute bottom-6 left-6 right-6 z-[1000] pointer-events-none"
            >
              <div
                v-motion
                :key="selectedIdx"
                :initial="{ opacity: 0, y: 20 }"
                :enter="{ 
                  opacity: 1, 
                  y: 0, 
                  transition: { duration: 500, ease: 'backOut' } 
                }"
                class="bg-black/80 backdrop-blur-md border border-gold/20 p-5 rounded-xl shadow-2xl"
              >
                <div class="flex items-center gap-3 mb-2">
                  <div class="w-8 h-[1px] bg-gold/50"></div>
                  <p class="text-gold text-[10px] font-bold uppercase tracking-[0.2em]">
                    Emplacement Sélectionné
                  </p>
                </div>
                <p class="text-white font-medium text-lg">
                  {{ locations[selectedIdx].location }}
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
:deep(.leaflet-control-attribution) {
  background: rgba(0, 0, 0, 0.5) !important;
  color: #666 !important;
}
:deep(.leaflet-bar) {
  border: 1px solid rgba(212, 175, 55, 0.2) !important;
}
:deep(.leaflet-bar a) {
  background-color: #111 !important;
  color: #d4af37 !important;
  border-bottom: 1px solid rgba(212, 175, 55, 0.2) !important;
}
:deep(.leaflet-bar a:hover) {
  background-color: #d4af37 !important;
  color: #000 !important;
}
</style>
