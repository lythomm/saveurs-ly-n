<script setup lang="ts">
import { X, ArrowLeft } from 'lucide-vue-next'

defineProps<{
  show: boolean
}>()

const emit = defineEmits(['close'])
</script>

<template>
  <Transition
    enter-active-class="transition duration-300 ease-out"
    enter-from-class="opacity-0 scale-95"
    enter-to-class="opacity-100 scale-100"
    leave-active-class="transition duration-200 ease-in"
    leave-from-class="opacity-100 scale-100"
    leave-to-class="opacity-0 scale-95"
  >
    <div v-if="show" class="fixed inset-0 z-[100] overflow-y-auto bg-[#0a0a0a]">
      <!-- Header -->
      <header class="sticky top-0 bg-[#0a0a0a]/80 backdrop-blur-md border-b border-white/5 py-4 px-6 flex justify-between items-center z-10">
        <button 
          @click="emit('close')"
          class="flex items-center gap-2 text-gray-400 hover:text-gold transition-colors text-sm font-medium"
        >
          <ArrowLeft :size="18" />
          Retour au site
        </button>
        <button 
          @click="emit('close')"
          class="w-10 h-10 rounded-full bg-white/5 flex items-center justify-center text-gray-400 hover:text-white transition-all"
        >
          <X :size="20" />
        </button>
      </header>

      <main class="container mx-auto px-6 py-16 max-w-4xl">
        <!-- Mentions Légales -->
        <section id="mentions-legales" class="mb-20">
          <h1 class="text-4xl font-display mb-12 gold-gradient">Mentions Légales</h1>
          
          <div class="space-y-10 text-gray-300 leading-relaxed">
            <div>
              <h2 class="text-xl font-bold text-white mb-4">1. Éditeur du site</h2>
              <p>
                Le site internet <strong>Saveurs de LyN</strong> est édité par l'entreprise individuelle [NOM DE L'ENTREPRISE], 
                domiciliée à [ADRESSE DU SIÈGE SOCIAL].
              </p>
              <ul class="mt-4 space-y-2">
                <li><strong>SIRET :</strong> [VOTRE NUMÉRO SIRET]</li>
                <li><strong>Responsable de la publication :</strong> Nouxiaxang Ly</li>
                <li><strong>Contact :</strong> 06 50 10 70 30</li>
                <li><strong>Email :</strong> nouxiaxang.ly@gmail.com</li>
              </ul>
            </div>

            <div>
              <h2 class="text-xl font-bold text-white mb-4">2. Hébergement</h2>
              <p>
                Le site est hébergé par [NOM DE L'HÉBERGEUR (ex: Vercel, Netlify, Hostinger)], 
                dont le siège social est situé à [ADRESSE DE L'HÉBERGEUR].
              </p>
            </div>

            <div>
              <h2 class="text-xl font-bold text-white mb-4">3. Propriété intellectuelle</h2>
              <p>
                L'ensemble du contenu de ce site (textes, images, logos, vidéos) est la propriété exclusive de Saveurs de LyN, 
                sauf mention contraire. Toute reproduction, distribution ou modification est interdite sans accord préalable écrit.
              </p>
            </div>

            <div>
              <h2 class="text-xl font-bold text-white mb-4">4. Activité Food Truck</h2>
              <p>
                L'activité de vente de nourriture nomade est soumise aux réglementations sanitaires en vigueur. 
                Saveurs de LyN dispose des autorisations nécessaires pour l'occupation du domaine public et le respect des normes d'hygiène alimentaire.
              </p>
            </div>
          </div>
        </section>

        <!-- Politique de Confidentialité -->
        <section id="politique-confidentialite">
          <h1 class="text-4xl font-display mb-12 gold-gradient">Politique de Confidentialité</h1>
          
          <div class="space-y-10 text-gray-300 leading-relaxed">
            <div>
              <h2 class="text-xl font-bold text-white mb-4">1. Collecte des données</h2>
              <p>
                Nous collectons des informations lorsque vous utilisez notre formulaire de contact ou que vous nous appelez :
              </p>
              <ul class="list-disc list-inside mt-4 space-y-2 ml-4">
                <li>Nom et prénom</li>
                <li>Adresse e-mail</li>
                <li>Numéro de téléphone</li>
                <li>Détails de l'évènement (pour les demandes de traiteur)</li>
              </ul>
            </div>

            <div>
              <h2 class="text-xl font-bold text-white mb-4">2. Utilisation des informations</h2>
              <p>
                Toutes les informations que nous recueillons auprès de vous peuvent être utilisées pour :
              </p>
              <ul class="list-disc list-inside mt-4 space-y-2 ml-4">
                <li>Vous contacter par e-mail ou téléphone</li>
                <li>Répondre à vos demandes de devis ou de privatisation</li>
                <li>Améliorer nos services et nos offres</li>
              </ul>
            </div>

            <div>
              <h2 class="text-xl font-bold text-white mb-4">3. Conservation des données</h2>
              <p>
                Vos données personnelles sont conservées pendant une durée de 3 ans à compter du dernier contact, 
                sauf obligation légale de conservation plus longue.
              </p>
            </div>

            <div>
              <h2 class="text-xl font-bold text-white mb-4">4. Vos droits</h2>
              <p>
                Conformément au RGPD, vous disposez d'un droit d'accès, de rectification, de portabilité et d'effacement de vos données. 
                Pour exercer ces droits, vous pouvez nous contacter à l'adresse suivante : <strong>nouxiaxang.ly@gmail.com</strong>.
              </p>
            </div>

            <div>
              <h2 class="text-xl font-bold text-white mb-4">5. Cookies</h2>
              <p>
                Ce site utilise des cookies techniques nécessaires à son bon fonctionnement. Nous pouvons également utiliser des outils d'analyse 
                (comme Google Analytics) pour mesurer l'audience du site, de manière anonymisée.
              </p>
            </div>
          </div>
        </section>
      </main>

      <!-- Footer for the legal page -->
      <footer class="py-12 border-t border-white/5 text-center text-gray-500 text-sm">
        <p>© {{ new Date().getFullYear() }} Saveurs de LyN - Cuisine Asiatique Artisanale</p>
      </footer>
    </div>
  </Transition>
</template>

<style scoped>
.font-display {
  font-family: var(--font-display);
}

.gold-gradient {
  background: linear-gradient(135deg, #d4af37 0%, #f9e29d 50%, #d4af37 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
</style>
