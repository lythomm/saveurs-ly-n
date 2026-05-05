<script setup lang="ts">
import { ref } from "vue";
import { ChevronDown } from "lucide-vue-next";

const faqs = [
  {
    question:
      "Proposez-vous la privatisation de foodtruck pour mariage à Lyon ?",
    answer:
      "Oui, Saveurs de Ly'N propose la privatisation complète de son foodtruck asiatique pour vos mariages, anniversaires et événements d'entreprise dans toute la région lyonnaise.",
  },
  {
    question: "Quels jours êtes-vous présents sur les marchés ?",
    answer:
      "Vous pouvez retrouver notre foodtruck au marché de Millery le samedi matin, et notre foodtruck au marché de Charly le dimanche matin.",
  },
  {
    question: "Faites-vous des plats asiatiques à emporter ?",
    answer:
      "Absolument ! Tous nos plats, y compris nos fameux nems et bo bun à emporter, sont préparés maison et disponibles directement sur les marchés ou sur commande.",
  },
  {
    question: "Faites-vous service traiteur asiatique à Lyon ?",
    answer:
      "Oui, en plus du foodtruck, nous proposons un service traiteur asiatique sur mesure pour vos réceptions privées et professionnelles autour de Lyon.",
  },
];

const openIndex = ref<number | null>(null);

const toggleFaq = (index: number) => {
  openIndex.value = openIndex.value === index ? null : index;
};
</script>

<template>
  <section id="faq" class="py-24 bg-[#111] overflow-hidden">
    <div class="container mx-auto px-6">
      <div class="max-w-4xl mx-auto">
        <div class="text-center mb-16">
          <h2 class="text-3xl md:text-5xl font-display mb-4 gold-gradient">
            Questions Fréquentes
          </h2>
          <div class="w-24 h-1 bg-gold rounded-2xl mx-auto"></div>
        </div>

        <div class="space-y-4">
          <!-- Accordion Item -->
          <div
            v-for="(faq, index) in faqs"
            :key="index"
            class="bg-white/5 border border-white/10 rounded-2xl overflow-hidden transition-all duration-300"
          >
            <button
              @click="toggleFaq(index)"
              class="w-full px-6 py-5 flex items-center justify-between text-left focus:outline-none cursor-pointer"
            >
              <h3 class="text-lg font-medium text-white pr-8">
                {{ faq.question }}
              </h3>
              <ChevronDown
                :size="20"
                class="text-gold transition-transform duration-300 flex-shrink-0"
                :class="{ 'rotate-180': openIndex === index }"
              />
            </button>

            <div
              class="grid transition-all duration-300 ease-in-out"
              :class="
                openIndex === index
                  ? 'grid-rows-[1fr] opacity-100'
                  : 'grid-rows-[0fr] opacity-0'
              "
            >
              <div class="overflow-hidden">
                <p class="px-6 pb-6 text-gray-400 leading-relaxed">
                  {{ faq.answer }}
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
.font-display {
  font-family: var(--font-display);
}
</style>
