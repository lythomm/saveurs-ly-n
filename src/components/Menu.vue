<script setup lang="ts">
const categories = [
  {
    title: "Entrées",
    items: [
      {
        name: "Nems au poulet ou porc (x3)",
        price: "4,00 €",
        allergens: "Soja",
      },
      {
        name: "Nems aux légumes (x3)",
        price: "3,50 €",
        allergens: "Gluten, Soja",
      },
      { name: "Samossa de bœuf (x3)", price: "4,00 €", allergens: "Gluten" },
      {
        name: "Triangle aux fromages (x3)",
        price: "4,00 €",
        allergens: "Gluten, Lactose",
      },
      {
        name: "Rouleau de printemps (Poulet/Crevettes)",
        price: "3,00 €",
        allergens: "Crustacés, Mollusques",
      },
    ],
  },
  {
    title: "Plats sur commande",
    items: [
      { name: "Bo Bun", price: "12,00 €", allergens: "Arachide" },
      {
        name: "Nouilles sautées poulet",
        price: "12,00 €",
        allergens: "Œuf, Arachide, Soja",
      },
      { name: "Bœuf Loc Lac", price: "12,00 €", allergens: "Œuf" },
      {
        name: "Pad Thaï (Légumes-œuf / Crevettes / Bœuf / Porc / Poulet)",
        price: "12,00 €",
        allergens: "Œuf, Arachide, Soja, Crustacé",
      },
    ],
  },
  {
    title: "Autres",
    items: [
      {
        name: "Banh Mi (Poulet ou Porc)",
        price: "7,00 €",
        allergens: "Gluten",
      },
      {
        name: "Banh Bao (Poulet ou Porc)",
        price: "5,00 €",
        allergens: "Gluten, Œuf",
      },
    ],
  },
  {
    title: "Desserts",
    items: [
      {
        name: "Fleurs de Lotus (x4)",
        price: "4,00 €",
        allergens: "Gluten, Graines de sésame, Œuf",
      },
      {
        name: "Roulé au Pandan (x2)",
        price: "4,00 €",
        allergens: "Gluten, Lait, Œuf",
      },
      {
        name: "Perles de coco (x3)",
        price: "4,00 €",
        allergens: "Graines de sésame",
      },
      {
        name: "Boules de sésame (x3)",
        price: "4,00 €",
        allergens: "Graines de sésame",
      },
    ],
  },
  {
    title: "Boissons",
    items: [
      {
        name: "Bubble Tea aux choix (Mangue, Pêche, Thé Jasmin)",
        price: "6,00 €",
        allergens: "Lactose",
      },
      {
        name: "Nab Van (Boisson 3 couleurs)",
        price: "6,00 €",
        allergens: "Contient du lait de coco",
      },
      { name: "Café", price: "1,30 €" },
    ],
  },
];
</script>

<template>
  <section id="menu" class="py-24 relative overflow-hidden bg-[#0a0a0a]">
    <!-- Background Motif Pattern -->
    <div
      class="absolute inset-0 opacity-[0.03] pointer-events-none"
      style="
        background-image: url(&quot;/menu-pattern.png&quot;);
        background-size: 400px;
        background-repeat: repeat;
        mask-image:
          radial-gradient(ellipse at center, black 20%, transparent 75%),
          linear-gradient(
            to bottom,
            transparent,
            black 15%,
            black 85%,
            transparent
          );
        -webkit-mask-image:
          radial-gradient(ellipse at center, black 20%, transparent 75%),
          linear-gradient(
            to bottom,
            transparent,
            black 15%,
            black 85%,
            transparent
          );
        mask-composite: intersect;
        -webkit-mask-composite: source-in;
      "
    ></div>

    <div class="container mx-auto px-6 relative z-10">
      <div class="flex flex-col items-center mb-16">
        <h2
          class="text-3xl md:text-5xl font-display mb-4 gold-gradient text-center"
        >
          Notre Menu Traiteur Asiatique
        </h2>
        <div class="w-24 h-1 bg-gold rounded-2xl mx-auto"></div>
      </div>

      <div
        class="max-w-6xl mx-auto grid md:grid-cols-2 gap-x-12 lg:gap-x-24 gap-y-16"
      >
        <div
          v-for="(cat, idx) in categories"
          :key="cat.title"
          v-motion
          :initial="{ opacity: 0, y: 30 }"
          :visible="{
            opacity: 1,
            y: 0,
            transition: { delay: idx * 100, duration: 600 },
          }"
          class="space-y-8"
        >
          <div class="flex items-center gap-6">
            <h3
              class="text-2xl font-display font-bold text-gold whitespace-nowrap"
            >
              {{ cat.title.toUpperCase() }}
            </h3>
            <div class="h-px bg-gold/20 flex-1"></div>
          </div>

          <div class="grid gap-6">
            <div
              v-for="item in cat.items"
              :key="item.name"
              class="flex justify-between items-start border-b border-white/5 pb-4 group last:border-0"
            >
              <div class="flex-1 mr-8">
                <div class="flex items-baseline gap-4">
                  <span
                    class="text-white group-hover:text-gold transition-colors text-lg font-medium leading-tight"
                    >{{ item.name }}</span
                  >
                  <div
                    class="flex-1 border-b border-dotted border-white/10 group-hover:border-gold/30 transition-colors hidden md:block"
                  ></div>
                </div>
                <span
                  v-if="item.allergens"
                  class="text-[11px] text-gray-500 uppercase tracking-widest block mt-2"
                >
                  Allergènes : {{ item.allergens }}
                </span>
              </div>
              <div class="text-gold-light font-mono text-lg whitespace-nowrap">
                {{ item.price }}
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
