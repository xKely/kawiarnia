<!-- src/components/Gallery.vue -->
<template>
  <section class="gallery-neo" ref="galleryRef">
    
    <div class="gallery-header" ref="headerRef">
      <h2 class="title">Nasze <span class="highlight">Specjały</span></h2>
      <p class="subtitle">Pyszności prosto z naszego menu retro.</p>
    </div>

    <div class="gallery-grid">
      <div 
        v-for="item in galleryItems" 
        :key="item.id" 
        :class="['gallery-item', item.className]"
      >
        <div class="polaroid">
          <img :src="item.src" :alt="item.alt" />
          <div class="polaroid-caption">{{ item.caption }}</div>
        </div>
      </div>
    </div>
    
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

const galleryRef = ref(null);
const headerRef = ref(null);

// Dynamiczna lista zdjęć - do łatwego powiązania z menu
const galleryItems = ref([
  {
    id: 1,
    src: "/sweet-strawberry-tea.jpg",
    className: "n1",
    alt: "Sweet Strawberry Tea",
    caption: "Sweet Strawberry Tea 🍰"
  },
  {
    id: 2,
    src: "/sernik-truskawkowa-rozkosz.jpg",
    className: "n2",
    alt: "Sernik „Truskawkowa Rozkosz”",
    caption: "Sernik „Truskawkowa Rozkosz” 🍓"
  },
  {
    id: 3,
    src: "/sernik-z-lodami.jpg",
    className: "n3",
    alt: "Sernik „Truskawkowa Rozkosz” z lodami",
    caption: "Sernik „Truskawkowa Rozkosz” z lodami 🥞"
  },
  {
    id: 4,
    src: "/strawberry-matcha.jpg",
    className: "n5",
    alt: "Strawberry Matcha",
    caption: "Strawberry Matcha 🥯"
  },
  {
    id: 5,
    src: "/truskawcino.jpg",
    className: "n6",
    alt: "Truskawcino",
    caption: "Truskawcino ☕"
  },
  {
    id: 6,
    src: "/latte-retro.jpg",
    className: "n7",
    alt: "Latte Retro",
    caption: "Latte Retro 🌟"
  }
]);

onMounted(() => {
  // 1. Animacja wejścia nagłówka
  gsap.fromTo(headerRef.value,
    { y: 50, opacity: 0 },
    {
      y: 0, opacity: 1, duration: 0.8, ease: 'back.out(1.5)',
      scrollTrigger: {
        trigger: galleryRef.value,
        start: "top 80%",
      }
    }
  );

  // 2. Kaskadowe (stagger) "wyskakiwanie" polaroidów z różnymi rotacjami
  gsap.fromTo(".gallery-item",
    { scale: 0.5, opacity: 0, rotation: () => gsap.utils.random(-20, 20) },
    {
      scale: 1, 
      opacity: 1, 
      rotation: (index, target) => {
        if (target.classList.contains('n1')) return -4;
        if (target.classList.contains('n2')) return 3;
        if (target.classList.contains('n3')) return -2;
        if (target.classList.contains('n4')) return 5;
        if (target.classList.contains('n5')) return -5;
        if (target.classList.contains('n6')) return 2;
        if (target.classList.contains('n7')) return -3;
        return 0;
      },
      duration: 0.8,
      stagger: 0.15,
      ease: 'back.out(1.7)',
      scrollTrigger: {
        trigger: ".gallery-grid",
        start: "top 75%",
      }
    }
  );
});
</script>

<style scoped>
/* GŁÓWNA SEKCJA Z TŁEM W KRATKĘ */
.gallery-neo {
  padding: 120px 5vw;
  background-color: #FFF;
  /* Retro zeszytowa kratka */
  background-image: 
    linear-gradient(#EAEAEA 2px, transparent 2px),
    linear-gradient(90deg, #EAEAEA 2px, transparent 2px);
  background-size: 50px 50px;
  position: relative;
  border-bottom: 4px solid #111;
}

/* --- NAGŁÓWEK --- */
.gallery-header {
  text-align: center;
  margin-bottom: 80px;
}

.title {
  font-family: 'Outfit', sans-serif;
  font-size: clamp(3rem, 6vw, 5rem);
  font-weight: 900;
  color: #111;
  text-transform: uppercase;
  margin-bottom: 15px;
}

.highlight {
  font-family: 'Pacifico', cursive;
  color: #90EE90; /* Light Green */
  text-transform: none;
  font-weight: normal;
  display: inline-block;
  /* Gruby czarny obrys (Stroke) i twardy cień */
  text-shadow: 
    -2px -2px 0 #111, 2px -2px 0 #111, -2px 2px 0 #111, 2px 2px 0 #111,
    6px 6px 0px #D2143A; /* Czerwony cień */
  transform: rotate(-3deg);
}

.subtitle {
  font-family: 'Outfit', sans-serif;
  font-size: 1.2rem;
  font-weight: 600;
  color: #333;
  background-color: #FFFFE0;
  display: inline-block;
  padding: 5px 15px;
  border: 2px solid #111;
  box-shadow: 4px 4px 0px #111;
  transform: rotate(1deg);
}

/* --- SIATKA GALERII --- */
.gallery-grid {
  max-width: 1300px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 40px;
  padding: 20px; /* Miejsce na cienie */
}

/* --- POLAROIDY --- */
.gallery-item {
  display: flex;
  justify-content: center;
  transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  cursor: crosshair; /* Ciekawy kursor dla elementu interaktywnego */
}

.polaroid {
  background-color: #FFF;
  padding: 15px 15px 60px 15px; /* Duży dół na podpis (jak polaroid) */
  border: 4px solid #111;
  border-radius: 8px; /* Lekkie zaokrąglenie, ale wciąż kanciasto */
  width: 100%;
  max-width: 350px;
  position: relative;
  transition: all 0.3s ease;
}

/* Zdjęcie wewnątrz polaroida */
.polaroid img {
  width: 100%;
  height: 300px;
  object-fit: cover;
  border: 3px solid #111;
  border-radius: 4px;
  filter: contrast(1.1) saturate(1.2); /* Lekki filtr retro na zdjęcia */
  background-color: #EEE; /* Fallback zanim załaduje się zdjęcie */
}

/* Podpis na zdjęciu */
.polaroid-caption {
  position: absolute;
  bottom: 15px;
  left: 0;
  width: 100%;
  text-align: center;
  font-family: 'Pacifico', cursive;
  font-size: 1.1rem;
  color: #111;
}

/* --- KOLORY CIENI I ROTACJE DLA KONKRETNYCH ZDJĘĆ --- */
/* Z biznesplanu: Pink, Red, Green, Yellow */

.n1 { transform: rotate(-4deg); }
.n1 .polaroid { box-shadow: 12px 12px 0px #F4C2C2; } /* Baby Pink */

.n2 { transform: rotate(3deg); margin-top: 40px; } /* Przesunięcie w dół rozbija idealną siatkę */
.n2 .polaroid { box-shadow: 12px 12px 0px #D2143A; } /* Strawberry Red */

.n3 { transform: rotate(-2deg); }
.n3 .polaroid { box-shadow: 12px 12px 0px #90EE90; } /* Light Green */

.n4 { transform: rotate(5deg); margin-top: -20px; }
.n4 .polaroid { box-shadow: 12px 12px 0px #FFFFE0; } /* Delicate Yellow */

.n5 { transform: rotate(-5deg); margin-top: 30px; }
.n5 .polaroid { box-shadow: 12px 12px 0px #D2143A; }

.n6 { transform: rotate(2deg); }
.n6 .polaroid { box-shadow: 12px 12px 0px #F4C2C2; }

.n7 { transform: rotate(-3deg); margin-top: -10px; }
.n7 .polaroid { box-shadow: 12px 12px 0px #90EE90; }

/* HOVER EFFECT - ZDJĘCIE OŻYWA */
.gallery-item:hover {
  z-index: 10; /* Wysuwa się na wierzch */
}

.gallery-item:hover .polaroid {
  transform: rotate(0deg) scale(1.05) translateY(-10px) !important;
  box-shadow: 18px 18px 0px #111; /* Zmiana cienia na potężny czarny */
}

/* RWD - MOBILE */
@media (max-width: 768px) {
  .gallery-grid {
    grid-template-columns: 1fr;
    gap: 50px;
  }
  
  .gallery-item {
    margin-top: 0 !important; /* Resetujemy marginesy na telefonach, żeby uniknąć dziur w układzie */
  }

  .polaroid {
    max-width: 100%;
  }
  
  .title {
    line-height: 1.2;
  }
}
</style>