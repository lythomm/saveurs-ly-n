<script setup lang="ts">
import logoUrl from "../assets/logo.png";
import heroBgUrl from "../assets/hero-bg.png";
import { onMounted, reactive, ref } from "vue";

const heroRef = ref<HTMLElement | null>(null);
const mouse = reactive({ x: 0, y: 0, tiltX: 0, tiltY: 0, lerpX: 0, lerpY: 0 });

const handleMouseMove = (e: MouseEvent) => {
  if (!heroRef.value) return;
  const { clientX, clientY } = e;
  const { left, top, width, height } = heroRef.value.getBoundingClientRect();

  // Normalize coordinates (-1 to 1)
  const x = ((clientX - left) / width) * 2 - 1;
  const y = ((clientY - top) / height) * 2 - 1;

  mouse.x = x;
  mouse.y = y;

  // Tilt values for 3D effect
  mouse.tiltX = y * 8;
  mouse.tiltY = -x * 8;
};

// Smooth mouse tracking
const updateLerp = () => {
  mouse.lerpX += (mouse.x - mouse.lerpX) * 0.08;
  mouse.lerpY += (mouse.y - mouse.lerpY) * 0.08;
  requestAnimationFrame(updateLerp);
};

const titlePart1Words = "L'excellence du".split(" ");
const titlePart2Words = "Foodtruck Asiatique".split(" ");
const titlePart3Words = ["à", "Lyon", "&", "alentours"];

onMounted(() => {
  updateLerp();

  const schema = {
    "@context": "https://schema.org",
    "@type": "FoodEstablishment",
    name: "Saveurs de Ly'N",
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
    ref="heroRef"
    @mousemove="handleMouseMove"
    class="relative min-h-screen flex items-center justify-center overflow-hidden py-20"
  >
    <!-- Background with CSS Animation -->
    <div
      class="absolute inset-0 z-0 bg-cover bg-center bg-no-repeat opacity-50"
      :style="{
        backgroundImage: `url(${heroBgUrl})`,
        transform: `scale(1.1) translate(${mouse.lerpX * -40}px, ${mouse.lerpY * -40}px)`,
        transition: 'transform 1s ease-out',
      }"
    ></div>

    <!-- Floating Particles -->
    <div class="absolute inset-0 z-[1] pointer-events-none opacity-20">
      <div
        v-for="i in 12"
        :key="i"
        class="absolute rounded-full bg-gold/40 blur-[2px] animate-float-particle"
        :style="{
          left: `${Math.random() * 100}%`,
          top: `${Math.random() * 100}%`,
          width: `${Math.random() * 6 + 2}px`,
          height: `${Math.random() * 6 + 2}px`,
          animationDuration: `${Math.random() * 10 + 15}s`,
          animationDelay: `${Math.random() * -20}s`,
          transform: `translate(${mouse.lerpX * (Math.random() * 60 - 30)}px, ${mouse.lerpY * (Math.random() * 60 - 30)}px)`,
        }"
      ></div>
    </div>

    <!-- Animated Gradient Overlays -->
    <div
      class="absolute inset-0 bg-gradient-to-b from-[#0a0a0a]/80 via-transparent to-[#0a0a0a] z-[1]"
    ></div>
    <div
      class="absolute inset-0 bg-gradient-to-r from-[#0a0a0a]/60 via-transparent to-[#0a0a0a]/60 z-[1]"
    ></div>

    <div class="container mx-auto px-6 relative z-10">
      <div class="grid lg:grid-cols-2 gap-16 items-center">
        <!-- Left Content: Text & Logo -->
        <div
          class="flex flex-col items-center lg:items-start text-center lg:text-left"
        >
          <!-- Title Animation with Unique Keys -->
          <h1
            class="text-4xl md:text-6xl xl:text-7xl font-display font-light mb-8 tracking-tight leading-[1.1]"
          >
            <div class="overflow-visible pb-2">
              <div
                class="flex flex-wrap justify-center lg:justify-start gap-x-[0.3em]"
              >
                <span
                  v-for="(word, i) in titlePart1Words"
                  :key="'p1-' + i"
                  v-motion
                  :initial="{ y: 50, opacity: 0 }"
                  :enter="{
                    y: 0,
                    opacity: 1,
                    transition: { duration: 800, delay: 400 + i * 100 },
                  }"
                  class="inline-block"
                >
                  {{ word }}
                </span>
              </div>
            </div>

            <div class="mt-4 overflow-visible py-2">
              <div
                class="flex flex-wrap justify-center lg:justify-start gap-x-[0.3em]"
              >
                <span
                  v-for="(word, i) in titlePart2Words"
                  :key="'p2-' + i"
                  v-motion
                  :initial="{ y: 50, opacity: 0 }"
                  :enter="{
                    y: 0,
                    opacity: 1,
                    transition: { duration: 800, delay: 800 + i * 100 },
                  }"
                  class="gold-gradient italic font-normal inline-block relative px-1"
                >
                  {{ word }}
                </span>
              </div>
            </div>
          </h1>

          <div
            class="text-3xl md:text-4xl mt-6 opacity-80 overflow-hidden py-1"
          >
            <div
              class="flex flex-wrap justify-center lg:justify-start gap-x-[0.3em]"
            >
              <span
                v-for="(word, i) in titlePart3Words"
                :key="'p3-' + i"
                v-motion
                :initial="{ y: 40, opacity: 0 }"
                :enter="{
                  y: 0,
                  opacity: 1,
                  transition: { duration: 800, delay: 1200 + i * 100 },
                }"
                class="inline-block font-light"
              >
                {{ word }}
              </span>
            </div>
          </div>

          <!-- Subtitle Animation -->
          <p
            v-motion
            :initial="{ opacity: 0, y: 30, filter: 'blur(10px)' }"
            :enter="{
              opacity: 1,
              y: 0,
              filter: 'blur(0px)',
              transition: {
                delay: 1800,
                duration: 1200,
                ease: [0.16, 1, 0.3, 1],
              },
            }"
            class="text-lg md:text-xl text-gray-400 max-w-2xl mb-12 font-light leading-relaxed"
          >
            Saveurs de Ly'N vous propose une cuisine authentique et raffinée.
            Nems croustillants, Bo Bun parfumés et spécialités maison pour vos
            événements privés ou professionnels.
          </p>

          <!-- CTA Buttons Animation -->
          <div
            v-motion
            :initial="{ opacity: 0, y: 40, scale: 0.95 }"
            :enter="{
              opacity: 1,
              y: 0,
              scale: 1,
              transition: {
                delay: 2100,
                duration: 1200,
                ease: [0.16, 1, 0.3, 1],
              },
            }"
            class="flex flex-col sm:flex-row gap-6 w-full sm:w-auto"
          >
            <a
              href="#menu"
              class="relative group overflow-hidden gold-border px-10 py-5 rounded-2xl text-gold font-bold transition-all duration-500 hover:text-black text-center"
            >
              <div
                class="absolute inset-0 bg-gold translate-y-full group-hover:translate-y-0 transition-transform duration-500 ease-[0.22, 1, 0.36, 1]"
              ></div>
              <span class="relative z-10 tracking-[0.2em] text-xs uppercase"
                >DÉCOUVRIR LE MENU</span
              >
              <!-- Hover Shimmer -->
              <div
                class="absolute inset-0 w-full h-full bg-gradient-to-r from-transparent via-white/20 to-transparent -translate-x-full group-hover:animate-shimmer"
              ></div>
            </a>
            <a
              href="#contact"
              class="relative bg-white/5 border border-white/10 px-10 py-5 rounded-2xl text-white font-medium hover:bg-white/10 hover:border-white/30 transition-all duration-500 group text-center overflow-hidden"
            >
              <span
                class="tracking-[0.2em] text-xs uppercase group-hover:text-gold transition-colors relative z-10"
                >NOUS CONTACTER</span
              >
              <div
                class="absolute inset-0 bg-gold/5 scale-x-0 group-hover:scale-x-100 transition-transform duration-500 origin-left"
              ></div>
            </a>
          </div>
        </div>

        <!-- Right Content: Hero Image Animation with 3D Tilt -->
        <div
          v-motion
          :initial="{ opacity: 0, scale: 0.8, filter: 'blur(20px)' }"
          :enter="{
            opacity: 1,
            scale: 1,
            filter: 'blur(0px)',
            transition: {
              delay: 800,
              duration: 1500,
              ease: [0.22, 1, 0.36, 1],
            },
          }"
          class="hidden md:flex justify-center items-center relative perspective-1000"
        >
          <!-- Dynamic Glow -->
          <div
            class="absolute w-[120%] h-[120%] bg-gold/5 rounded-full blur-[100px] animate-slow-pulse transition-transform duration-1000 ease-out"
            :style="{
              transform: `translate(${mouse.lerpX * 40}px, ${mouse.lerpY * 40}px)`,
            }"
          ></div>

          <!-- Magnetic Hero Image Container -->
          <div
            class="relative transition-transform duration-500 ease-out preserve-3d group"
            :style="{
              transform: `rotateX(${mouse.tiltX}deg) rotateY(${mouse.tiltY}deg)`,
            }"
          >
            <!-- Background Golden Glare (Active on Hover) -->
            <div
              class="absolute inset-0 bg-[radial-gradient(circle,rgba(212,175,55,0.4)_0%,rgba(212,175,55,0)_70%)] opacity-0 group-hover:opacity-100 rounded-full blur-[60px] transition-opacity duration-700 pointer-events-none"
              :style="{
                transform: `translate(${mouse.lerpX * 40}px, ${mouse.lerpY * 40}px) scale(1.1)`,
              }"
            ></div>

            <!-- Intense Specular Glare -->
            <div
              class="absolute inset-4 bg-[radial-gradient(circle,rgba(255,255,255,0.2)_0%,rgba(212,175,55,0)_50%)] opacity-0 group-hover:opacity-100 rounded-full blur-xl transition-opacity duration-500 pointer-events-none"
              :style="{
                transform: `translate(${mouse.lerpX * 60}px, ${mouse.lerpY * 60}px) scale(0.8)`,
              }"
            ></div>

            <div
              class="absolute inset-0 bg-gradient-to-tr from-gold/20 via-transparent to-gold/20 rounded-full blur-2xl opacity-40 transition-transform duration-700"
              :style="{
                transform: `translate(${mouse.lerpX * 15}px, ${mouse.lerpY * 15}px)`,
              }"
            ></div>

            <div
              class="relative animate-float rounded-3xl group logo-glare-container w-fit mx-auto"
            >
              <img
                :src="logoUrl"
                alt="Saveurs de Ly'N Logo"
                class="w-full max-w-xs relative z-10 drop-shadow-[0_20px_60px_rgba(0,0,0,0.6)] transition-transform duration-1000"
              />
              <!-- Golden Glare Effect -->
              <div
                class="absolute inset-0 z-20 pointer-events-none logo-glare-effect"
                :style="{
                  maskImage: `url(${logoUrl})`,
                  webkitMaskImage: `url(${logoUrl})`,
                }"
              ></div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Scroll Indicator -->
    <div
      v-motion
      :initial="{ opacity: 0 }"
      :enter="{
        opacity: 1,
        transition: { delay: 2000, duration: 1000 },
      }"
      class="hidden md:flex absolute bottom-12 left-1/2 -translate-x-1/2 flex-col items-center gap-3"
    >
      <span
        class="text-sm text-gray-500 uppercase tracking-[0.4em] rotate-180 [writing-mode:vertical-lr]"
        >Scroll</span
      >
      <div
        class="w-[1px] h-12 bg-gradient-to-b from-gold/50 to-transparent relative overflow-hidden"
      >
        <div
          class="absolute top-0 left-0 w-full h-full bg-gold animate-scroll-line"
        ></div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.preserve-3d {
  transform-style: preserve-3d;
}

.perspective-1000 {
  perspective: 1000px;
}

@keyframes shimmer {
  0% {
    transform: translateX(-100%);
  }
  100% {
    transform: translateX(100%);
  }
}

.animate-shimmer {
  animation: shimmer 2s infinite linear;
}

@keyframes float-particle {
  0%,
  100% {
    transform: translate(0, 0);
  }
  25% {
    transform: translate(10px, -15px);
  }
  50% {
    transform: translate(-5px, -25px);
  }
  75% {
    transform: translate(-15px, -10px);
  }
}

.animate-float-particle {
  animation: float-particle 15s infinite ease-in-out;
}

@keyframes float {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-20px);
  }
}

.animate-float {
  animation: float 6s infinite ease-in-out;
}

@keyframes scroll-line {
  0% {
    transform: translateY(-100%);
  }
  100% {
    transform: translateY(100%);
  }
}

.animate-scroll-line {
  animation: scroll-line 2s infinite ease-in-out;
}

.animate-slow-pulse {
  animation: slow-pulse 4s infinite ease-in-out;
}

.logo-glare-container {
  mask-repeat: no-repeat;
  mask-size: contain;
}

.logo-glare-effect {
  mask-size: contain;
  mask-repeat: no-repeat;
  mask-position: center;
  background: linear-gradient(
    105deg,
    transparent 20%,
    rgba(255, 255, 255, 0.2) 35%,
    rgba(212, 175, 55, 0.7) 45%,
    rgba(255, 255, 255, 0.9) 50%,
    rgba(212, 175, 55, 0.7) 55%,
    rgba(255, 255, 255, 0.2) 65%,
    transparent 80%
  );
  background-size: 200% 100%;
  animation: logo-glare-sweep 5s infinite linear;
  mix-blend-mode: overlay;
  opacity: 0.8;
}

@keyframes logo-glare-sweep {
  0% {
    background-position: -200% 0;
  }
  100% {
    background-position: 200% 0;
  }
}

@keyframes slow-pulse {
  0%,
  100% {
    opacity: 0.2;
    transform: scale(1);
  }
  50% {
    opacity: 0.5;
    transform: scale(1.1);
  }
}
</style>
