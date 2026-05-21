<!-- src/views/Menu.vue -->
<template>
  <main class="menu-page">
    
    <!-- NAGŁÓWEK MENU -->
    <header class="menu-header" ref="headerRef">
      <div class="badge">Co podać?</div>
      <h1 class="title">Nasze <span class="highlight">Menu</span></h1>
      <p class="subtitle">Karty z naszymi propozycjami. Od klasycznego espresso po truskawkowe desery i śniadania.</p>
    </header>

    <!-- LISTA KATEGORII MENU -->
    <div class="menu-container" ref="containerRef">
      
      <div 
        class="menu-card" 
        v-for="(category, index) in menuData" 
        :key="index"
        :style="{ backgroundColor: category.bgColor, boxShadow: `10px 10px 0px ${category.shadowColor}` }"
      >
        <!-- Tytuł kategorii (ikona + tekst) -->
        <div class="category-header">
          <span class="category-icon">{{ category.icon }}</span>
          <h2>{{ category.title }}</h2>
        </div>

        <!-- Lista produktów w danej kategorii -->
        <ul class="items-list">
          <li class="item-row" v-for="(item, i) in category.items" :key="i">
            <div class="item-info">
              <h3 class="item-name">{{ item.name }}</h3>
              <p class="item-desc">{{ item.desc }}</p>
            </div>
            <div class="item-price">
              <span>{{ item.price }}</span>
            </div>
          </li>
        </ul>
      </div>

    </div>

    <!-- PŁYWAJĄCE DEKORACJE POP-ART W TLE (Wizualny smaczek) -->
    <div class="decor-star star-1">✦</div>
    <div class="decor-star star-2">✦</div>

  </main>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

// --- DANE MENU (Czysto i łatwo do edycji w przyszłości) ---
const menuData = [
  {
    title: "Kawy",
    icon: "☕",
    bgColor: "#F4C2C2", // Baby Pink
    shadowColor: "#D2143A", // Strawberry Red
    items: [
      { name: "Espresso", desc: "Klasyczna kawa przygotowywana z wysokiej jakości ziaren.", price: "12 zł" },
      { name: "Cappuccino", desc: "Kawa z mlekiem i puszystą pianką.", price: "16 zł" },
      { name: "Latte Retro", desc: "Autorskie latte podawane w wysokiej szklance inspirowanej stylem retro.", price: "20 zł" },
      { name: "Iced Latte Pink", desc: "Mrożona kawa z dodatkiem syropu truskawkowego.", price: "22 zł" }
    ]
  },
  {
    title: "Napoje autorskie",
    icon: "🍓",
    bgColor: "#FFFFE0", // Delicate Yellow
    shadowColor: "#111111", // Czarny
    items: [
      { name: "Truskawcino", desc: "Autorski napój na bazie truskawek i mleka.", price: "24 zł" },
      { name: "Strawberry Matcha", desc: "Napój łączący matchę z musem truskawkowym.", price: "25 zł" },
      { name: "Sweet Strawberry Tea", desc: "Herbata z dodatkiem owoców i syropu truskawkowego.", price: "18 zł" },
      { name: "Lemoniada truskawkowa", desc: "Orzeźwiająca lemoniada przygotowywana ze świeżych owoców.", price: "19 zł" }
    ]
  },
  {
    title: "Desery",
    icon: "🍰",
    bgColor: "#90EE90", // Light Green
    shadowColor: "#111111", // Czarny
    items: [
      { name: "Sernik „Truskawkowa Rozkosz”", desc: "Sernik z musem truskawkowym i dekoracją owocową.", price: "22 zł" },
      { name: "Gofry z truskawkami", desc: "Gofry podawane z owocami i bitą śmietaną.", price: "20 zł" },
      { name: "Pancakes retro", desc: "Puszyste pancakes inspirowane kuchnią amerykańską.", price: "26 zł" },
      { name: "Tarta truskawkowa", desc: "Krucha tarta z kremem waniliowym i owocami.", price: "18 zł" }
    ]
  },
  {
    title: "Śniadania",
    icon: "🥞",
    bgColor: "#F4C2C2", // Baby Pink
    shadowColor: "#111111", // Czarny
    items: [
      { name: "Croissant śniadaniowy", desc: "Croissant podawany z dodatkami.", price: "17 zł" },
      { name: "Tosty francuskie", desc: "Tosty z owocami i syropem.", price: "21 zł" },
      { name: "Bajgle", desc: "Bajgle z dodatkami wytrawnymi.", price: "23 zł" },
      { name: "Śniadanie amerykańskie", desc: "Zestaw inspirowany kuchnią amerykańską.", price: "29 zł" }
    ]
  },
  {
    title: "Pozycje sezonowe",
    icon: "🌟",
    bgColor: "#FFFFE0", // Delicate Yellow
    shadowColor: "#D2143A", // Strawberry Red
    items: [
      { name: "Zimowe napoje", desc: "Rozgrzewające napary i korzenne kawy w okresie zimowym.", price: "Oferta" },
      { name: "Świąteczne desery", desc: "Kultowe pierniki i ciasta pachnące świętami.", price: "Oferta" },
      { name: "Letnie lemoniady", desc: "Orzeźwiające kompozycje owocowe na upalne dni.", price: "Oferta" },
      { name: "Jesienne kawy smakowe", desc: "Kawy korzenne, dyniowe i orzechowe na jesienne chłody.", price: "Oferta" }
    ]
  }
];

const headerRef = ref(null);
const containerRef = ref(null);

onMounted(() => {
  // 1. Animacja wejścia nagłówka menu
  gsap.fromTo(headerRef.value.children,
    { y: 40, opacity: 0 },
    { y: 0, opacity: 1, duration: 0.8, stagger: 0.15, ease: 'back.out(1.5)', delay: 0.2 }
  );

  // 2. Kaskadowy wjazd kart z menu (ScrollTrigger)
  const cards = gsap.utils.toArray('.menu-card');
  
  cards.forEach((card, i) => {
    gsap.fromTo(card,
      { y: 100, opacity: 0, rotation: i % 2 === 0 ? 2 : -2 }, // Lekko naprzemienne kąty początkowe
      {
        y: 0,
        opacity: 1,
        rotation: 0,
        duration: 0.8,
        ease: 'back.out(1.2)',
        scrollTrigger: {
          trigger: card,
          start: "top 85%", // Karta zaczyna się pojawiać, gdy jej góra wejdzie w 85% ekranu
        }
      }
    );
  });
});
</script>

<style scoped>
/* GŁÓWNY KONTENER PODSTRONY */
.menu-page {
  min-height: 100vh;
  padding: 150px 5vw 100px;
  background-color: #FAFAFA; /* Bardzo jasne tło dla kontrastu */
  /* Delikatny retro pattern w kropki z tyłu (opcjonalny, subtelny) */
  background-image: radial-gradient(#DDD 1px, transparent 1px);
  background-size: 20px 20px;
  font-family: 'Outfit', sans-serif;
  position: relative;
  overflow: hidden;
}

/* --- NAGŁÓWEK --- */
.menu-header {
  text-align: center;
  max-width: 800px;
  margin: 0 auto 80px;
  position: relative;
  z-index: 10;
}

.badge {
  display: inline-block;
  font-weight: 800;
  font-size: 1rem;
  color: #FFF;
  background-color: #111;
  padding: 8px 24px;
  border-radius: 50px;
  text-transform: uppercase;
  margin-bottom: 20px;
  box-shadow: 4px 4px 0px #D2143A;
  transform: rotate(-2deg);
}

.title {
  font-size: clamp(3.5rem, 8vw, 5rem);
  font-weight: 900;
  color: #111;
  text-transform: uppercase;
  line-height: 1.1;
  margin-bottom: 20px;
}

.highlight {
  font-family: 'Pacifico', cursive;
  color: #D2143A;
  text-transform: none;
  font-weight: normal;
  display: block; /* Przenosi na nową linię dla potężnego efektu */
  text-shadow: 4px 4px 0px #111;
  transform: rotate(-3deg);
  margin-top: 5px;
}

.subtitle {
  font-size: 1.25rem;
  font-weight: 500;
  color: #444;
  line-height: 1.6;
}

/* --- KARTY MENU --- */
.menu-container {
  max-width: 1000px; /* Nie za szerokie, by tekst nie ciągnął się w nieskończoność */
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  gap: 60px;
  position: relative;
  z-index: 10;
}

.menu-card {
  border: 4px solid #111;
  border-radius: 24px;
  padding: 40px;
  transition: transform 0.3s ease;
}

.menu-card:hover {
  transform: translate(-4px, -4px) !important; /* Nadpisuje GSAP na hover */
}

.category-header {
  display: flex;
  align-items: center;
  gap: 15px;
  margin-bottom: 30px;
  padding-bottom: 20px;
  border-bottom: 4px solid #111;
}

.category-icon {
  font-size: 3rem;
  filter: drop-shadow(3px 3px 0px rgba(0,0,0,0.2));
}

.category-header h2 {
  font-size: 2.5rem;
  font-weight: 900;
  color: #111;
  text-transform: uppercase;
  letter-spacing: -1px;
}

/* --- POZYCJE W MENU --- */
.items-list {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 25px;
}

.item-row {
  display: flex;
  justify-content: space-between;
  align-items: flex-end; /* Ceny i tekst wyrównane do dołu */
  gap: 20px;
  position: relative;
}

/* Linia kropkowana łącząca tekst z ceną */
.item-row::after {
  content: '';
  position: absolute;
  bottom: 8px;
  left: 0;
  right: 0;
  border-bottom: 3px dotted #111;
  z-index: 1;
  opacity: 0.3;
}

.item-info {
  background-color: inherit; /* Przyjmuje kolor karty by zakryć kropki pod sobą */
  padding-right: 15px;
  position: relative;
  z-index: 2;
  max-width: 80%;
}

.item-name {
  font-size: 1.4rem;
  font-weight: 800;
  color: #111;
  margin-bottom: 5px;
}

.item-desc {
  font-size: 1rem;
  font-weight: 500;
  color: #444;
  line-height: 1.4;
}

.item-price {
  background-color: inherit;
  padding-left: 15px;
  position: relative;
  z-index: 2;
  flex-shrink: 0;
}

.item-price span {
  display: inline-block;
  font-weight: 900;
  font-size: 1.2rem;
  color: #FFF;
  background-color: #111;
  padding: 6px 16px;
  border-radius: 50px;
  border: 2px solid #111;
  box-shadow: 3px 3px 0px rgba(0,0,0,0.3);
  transform: rotate(2deg);
}

/* --- DEKORACJE TŁA (GWIAZDKI) --- */
.decor-star {
  position: absolute;
  font-size: 5rem;
  color: #FFFFE0;
  text-shadow: 2px 2px 0 #111;
  z-index: 1;
  pointer-events: none;
  opacity: 0.8;
}

.star-1 {
  top: 15%;
  left: 10%;
  transform: rotate(15deg);
}

.star-2 {
  bottom: 20%;
  right: 5%;
  color: #F4C2C2;
  transform: rotate(-10deg);
}

/* RWD - MOBILE */
@media (max-width: 768px) {
  .menu-page {
    padding: 130px 5vw 80px;
  }

  .menu-card {
    padding: 25px;
    border-width: 3px;
  }

  .category-header h2 {
    font-size: 1.8rem;
  }
  
  .category-icon {
    font-size: 2rem;
  }

  /* Na komórkach usuwamy linię kropkowaną i przenosimy cenę pod opis */
  .item-row {
    flex-direction: column;
    align-items: flex-start;
    gap: 10px;
  }

  .item-row::after {
    display: none;
  }

  .item-info {
    max-width: 100%;
    padding-right: 0;
  }

  .item-price {
    padding-left: 0;
    align-self: flex-start;
  }
}
</style>