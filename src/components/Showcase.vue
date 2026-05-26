<!-- src/components/Showcase.vue -->
<template>
  <section class="showcase-neo" ref="showcaseRef">
    
    <!-- Pływające elementy dekoracyjne w tle -->
    <div class="decor-shape pill" ref="decorPill"></div>
    <div class="decor-shape zigzag" ref="decorZigzag"></div>

    <div class="showcase-container">
      
      <!-- LEWA STRONA: OBRAZKI Z PARALAKSĄ -->
      <div class="visual-side">
        <!-- Retro naklejka -->
        <div class="retro-sticker" ref="stickerRef">
          <svg viewBox="0 0 100 100" class="sticker-text">
            <path d="M 50, 50 m -37, 0 a 37,37 0 1,1 74,0 a 37,37 0 1,1 -74,0" id="circle-path" fill="none"/>
            <text>
              <textPath href="#circle-path" startOffset="0%">• 100% AUTORSKIE • ŚWIEŻE WYPIEKI </textPath>
            </text>
          </svg>
          <span class="sticker-center">🍰</span>
        </div>

        <div class="img-wrapper img-front" ref="imgFrontRef">
          <img src="/pancakes.jpg" alt="Pancakes retro" class="brutalist-img" />
        </div>
        
        <div class="img-wrapper img-back" ref="imgBackRef">
          <img src="/latte.jpg" alt="Latte Retro" class="brutalist-img" />
        </div>
      </div>

      <!-- PRAWA STRONA: TEKST -->
      <div class="text-side" ref="textRef">
        <h2 class="title">
          Poczuj klimat <br>
          <span class="highlight-box">lat</span> 60.
        </h2>
        <p class="description">
          Stworzyliśmy przestrzeń w stylu retro lat 60. Odcienie baby pink, truskawkowa czerwień i detale z epoki.
        </p>
        <p class="description">
          Napijesz się u nas autorskiego Truskawcino albo klasycznej kawy. To miejsce stworzone do spotkań ze znajomymi i chillu przy dobrej muzyce.
        </p>
        
        <ul class="features-list">
          <li>Kawa z lokalnej palarni</li>
          <li>Codziennie świeże ciasta i desery</li>
          <li>Retro muzyka z lat 60.</li>
        </ul>
      </div>

    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

const showcaseRef = ref(null);
const textRef = ref(null);
const imgFrontRef = ref(null);
const imgBackRef = ref(null);
const stickerRef = ref(null);
const decorPill = ref(null);
const decorZigzag = ref(null);

onMounted(() => {
  // 1. Animacja wejścia tekstu po zescrollowaniu
  gsap.fromTo(textRef.value.children,
    { x: 50, opacity: 0 },
    {
      x: 0, opacity: 1, duration: 0.8, stagger: 0.15, ease: 'back.out(1.2)',
      scrollTrigger: {
        trigger: showcaseRef.value,
        start: "top 70%",
      }
    }
  );

  // 2. Paralaksa na głównym zdjęciu (Pancakes) - jedzie szybciej do góry
  gsap.fromTo(imgFrontRef.value,
    { y: 100 },
    {
      y: -50,
      ease: 'none',
      scrollTrigger: {
        trigger: showcaseRef.value,
        start: "top bottom",
        end: "bottom top",
        scrub: 1 // scrub sprawia, że animacja podąża za scrollem
      }
    }
  );

  // 3. Paralaksa na tylnym zdjęciu (Latte) - jedzie wolniej (tworzy głębię)
  gsap.fromTo(imgBackRef.value,
    { y: 50 },
    {
      y: 20,
      ease: 'none',
      scrollTrigger: {
        trigger: showcaseRef.value,
        start: "top bottom",
        end: "bottom top",
        scrub: 1.5
      }
    }
  );

  // 4. Obracająca się naklejka
  gsap.to(stickerRef.value, {
    rotation: 360,
    duration: 15,
    repeat: -1,
    ease: 'linear'
  });

  // 5. Ruchomne dekoracje w tle
  gsap.to(decorPill.value, {
    y: 40, rotation: 15, duration: 4, yoyo: true, repeat: -1, ease: 'sine.inOut'
  });
  gsap.to(decorZigzag.value, {
    y: -30, rotation: -10, duration: 5, yoyo: true, repeat: -1, ease: 'sine.inOut'
  });
});
</script>

<style scoped>
/* GŁÓWNA SEKCJA */
.showcase-neo {
  position: relative;
  background-color: #F4C2C2; /* Baby Pink z biznesplanu */
  padding: 150px 5vw;
  overflow: hidden;
  border-top: 4px solid #111; /* Grube oddzielenie od Hero */
  border-bottom: 4px solid #111;
}

/* TŁO - DEKORACJE POP-ART */
.decor-shape {
  position: absolute;
  border: 3px solid #111;
  box-shadow: 4px 4px 0px #111;
  z-index: 1;
}

.decor-shape.pill {
  width: 120px;
  height: 50px;
  background-color: #90EE90; /* Jasna zieleń */
  border-radius: 50px;
  top: 10%;
  left: 5%;
  transform: rotate(-15deg);
}

.decor-shape.zigzag {
  width: 80px;
  height: 80px;
  background-color: #FFFFE0; /* Żółty */
  clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
  bottom: 10%;
  right: 8%;
  transform: rotate(20deg);
}

.showcase-container {
  max-width: 1300px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 80px;
  align-items: center;
  position: relative;
  z-index: 5;
}

/* --- LEWA STRONA (ZDJĘCIA) --- */
.visual-side {
  position: relative;
  height: 600px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.img-wrapper {
  position: absolute;
  /* Brutalistyczne obramowanie i cień dla zdjęć */
  border: 4px solid #111;
  border-radius: 20px;
  overflow: hidden;
  background-color: #FFF;
}

.img-front {
  width: 60%;
  aspect-ratio: 3/4;
  bottom: 5%;
  right: 5%;
  z-index: 3;
  box-shadow: 12px 12px 0px #111;
  transform: rotate(-3deg);
}

.img-back {
  width: 55%;
  aspect-ratio: 4/5;
  top: 5%;
  left: 5%;
  z-index: 2;
  box-shadow: -10px 10px 0px #D2143A; /* Czerwony cień rzucony w lewo */
  transform: rotate(4deg);
}

.brutalist-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.4s ease;
}

.img-wrapper:hover .brutalist-img {
  transform: scale(1.05); /* Lekki zoom przy najechaniu */
}

/* OBRACAJĄCA SIĘ NAKLEJKA */
.retro-sticker {
  position: absolute;
  top: -20px;
  right: -20px;
  width: 140px;
  height: 140px;
  background-color: #FFFFE0;
  border: 3px solid #111;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 10;
  box-shadow: 6px 6px 0px #111;
}

.sticker-text {
  width: 100%;
  height: 100%;
  font-family: 'Outfit', sans-serif;
  font-weight: 800;
  font-size: 14px;
  letter-spacing: 2px;
  fill: #111;
  animation: spinSlow 10s linear infinite;
}

.sticker-center {
  position: absolute;
  font-size: 2.5rem;
}

/* --- PRAWA STRONA (TEKST) --- */
.text-side {
  color: #111;
  font-family: 'Outfit', sans-serif;
}

.title {
  font-size: clamp(2.5rem, 4vw, 4rem);
  font-weight: 900;
  line-height: 1.1;
  margin-bottom: 30px;
  text-transform: uppercase;
}

.highlight-box {
  display: inline-block;
  background-color: #D2143A; /* Czerwony marker */
  color: #FFF;
  padding: 0 15px;
  border: 3px solid #111;
  box-shadow: 6px 6px 0px #111;
  transform: rotate(-2deg);
  margin-top: 10px;
}

.description {
  font-size: 1.15rem;
  line-height: 1.7;
  margin-bottom: 20px;
  font-weight: 500;
  color: #222;
}

.description strong {
  background-color: #FFFFE0;
  padding: 0 4px;
  border: 1px solid #111;
  border-radius: 4px;
}

/* LISTA Z PTASZKAMI */
.features-list {
  list-style: none;
  margin-top: 30px;
}

.features-list li {
  font-size: 1.1rem;
  font-weight: 700;
  margin-bottom: 12px;
  display: flex;
  align-items: center;
  gap: 10px;
}

.features-list li::before {
  content: '★';
  color: #D2143A;
  font-size: 1.4rem;
  /* Tekstowy obrys dla gwiazdki */
  text-shadow: 1px 1px 0 #111, -1px -1px 0 #111, 1px -1px 0 #111, -1px 1px 0 #111;
}

/* RWD - MOBILE */
@media (max-width: 968px) {
  .showcase-container {
    grid-template-columns: 1fr;
    gap: 40px;
  }
  
  .visual-side {
    height: 500px;
    order: -1; /* Obrazki idą na górę */
  }
  
  .img-front {
    width: 70%;
    right: 0;
  }
  
  .img-back {
    width: 65%;
    left: 0;
  }
  
  .retro-sticker {
    width: 100px;
    height: 100px;
    top: -10px;
    right: 10px;
  }
  
  .sticker-center {
    font-size: 1.8rem;
  }
  
  .title {
    text-align: center;
  }
  
  .highlight-box {
    transform: rotate(0);
  }
}
</style>