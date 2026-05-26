<!-- src/components/Hero.vue -->
<template>
  <section class="hero-neo">
    <div class="hero-container">
      
      <!-- LEWA STRONA: TYPOGRAFIA I CTA -->
      <div class="hero-content">
        <div class="badge" ref="badgeRef">
          <span class="badge-icon">🍓</span> Otwarcie Roku w Krakowie
        </div>
        
        <h1 class="title" ref="titleRef">
          Truskawkowa<br>
          <span class="highlight">Rozkosz</span>
        </h1>
        
        <p class="subtitle" ref="subtitleRef">
          Retro kawiarnia w Nowej Hucie. Wpadnij na autorskie Truskawcino, usiądź w kultowym fotelu i poczuj klimat lat 60.
        </p>
        
        <div class="action-wrapper" ref="btnRef">
          <router-link to="/menu" class="btn-brutalist">
            Sprawdź Menu 
            <span class="arrow">➔</span>
          </router-link>
          <!-- Ozdobna gwiazdka w stylu pop-art -->
          <div class="decor-star" ref="starRef">✦</div>
        </div>
      </div>

      <!-- PRAWA STRONA: WIDEO W STYLIZOWANEJ RAMCE -->
      <div class="hero-visual" ref="visualRef">
        <div class="video-frame">
          <!-- Nakładka koloryzująca delikatnie wideo -->
          <div class="video-overlay"></div>
          <video autoplay loop muted playsinline class="hero-video">
            <source src="/cafe-bg.mp4" type="video/mp4" />
          </video>
        </div>
      </div>

    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import gsap from 'gsap';

const badgeRef = ref(null);
const titleRef = ref(null);
const subtitleRef = ref(null);
const btnRef = ref(null);
const visualRef = ref(null);
const starRef = ref(null);

onMounted(() => {
  const tl = gsap.timeline({ delay: 0.3 });

  // 1. Lewa strona wjeżdża z brutalistycznym "tupnięciem"
  tl.fromTo(badgeRef.value, 
    { x: -50, opacity: 0, rotation: -10 }, 
    { x: 0, opacity: 1, rotation: -3, duration: 0.6, ease: 'back.out(2)' }
  )
  .fromTo(titleRef.value, 
    { y: 50, opacity: 0 }, 
    { y: 0, opacity: 1, duration: 0.8, ease: 'power4.out' },
    "-=0.4"
  )
  .fromTo(subtitleRef.value, 
    { y: 20, opacity: 0 }, 
    { y: 0, opacity: 1, duration: 0.6, ease: 'power2.out' },
    "-=0.5"
  )
  .fromTo(btnRef.value,
    { scale: 0.8, opacity: 0 },
    { scale: 1, opacity: 1, duration: 0.6, ease: 'back.out(1.5)' },
    "-=0.3"
  )
  // 2. Prawa strona (wideo) "wskakuje" na miejsce z rotacją
  .fromTo(visualRef.value,
    { x: 100, y: 50, opacity: 0, rotation: 10 },
    { x: 0, y: 0, opacity: 1, rotation: 0, duration: 1, ease: 'back.out(1.2)' },
    "-=0.8"
  );

  // Animacja kręcącej się gwiazdki w nieskończoność
  gsap.to(starRef.value, {
    rotation: 360,
    duration: 10,
    repeat: -1,
    ease: 'linear'
  });
});
</script>

<style scoped>
/* GŁÓWNY KONTENER + TŁO KOMIKSOWE (Polka Dots) */
.hero-neo {
  min-height: 100vh;
  padding: 120px 5vw 60px; /* Odstęp od navbara */
  background-color: #FFFFE0; /* Delicate yellow */
  /* Retro kropki w kolorze Baby Pink */
  background-image: radial-gradient(#F4C2C2 2px, transparent 2px);
  background-size: 30px 30px;
  display: flex;
  align-items: center;
  overflow: hidden;
}

.hero-container {
  max-width: 1400px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 80px;
  align-items: center;
}

/* --- LEWA STRONA (TEKST) --- */
.hero-content {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  z-index: 10;
}

/* Retro etykietka */
.badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background-color: #90EE90; /* Light green */
  color: #111;
  font-family: 'Outfit', sans-serif;
  font-weight: 700;
  font-size: 0.9rem;
  padding: 8px 16px;
  border: 2px solid #111;
  border-radius: 50px;
  box-shadow: 4px 4px 0px #111;
  margin-bottom: 30px;
  transform: rotate(-3deg);
}

.badge-icon {
  font-size: 1.2rem;
}

/* Wielki Brutalistyczny Tytuł */
.title {
  font-family: 'Outfit', sans-serif;
  font-size: clamp(3rem, 6vw, 5.5rem);
  font-weight: 900;
  color: #111;
  line-height: 1.1;
  margin-bottom: 25px;
  text-transform: uppercase;
  letter-spacing: -2px;
}

.title .highlight {
  font-family: 'Pacifico', cursive; /* Przełamanie stylu na retro font */
  color: #D2143A;
  text-transform: none;
  font-weight: normal;
  display: inline-block;
  letter-spacing: 2px;
  /* Gruby biały obrys i twardy, podwójny cień */
  text-shadow: 
    -2px -2px 0 #FFF, 2px -2px 0 #FFF, -2px 2px 0 #FFF, 2px 2px 0 #FFF,
    6px 6px 0px #111;
  transform: rotate(-2deg);
  margin-top: 10px;
}

.subtitle {
  font-family: 'Outfit', sans-serif;
  font-size: 1.25rem;
  line-height: 1.6;
  color: #333;
  margin-bottom: 40px;
  max-width: 90%;
  font-weight: 500;
}

/* --- PRZYCISK (CTA) --- */
.action-wrapper {
  position: relative;
  display: inline-block;
}

.btn-brutalist {
  display: inline-flex;
  align-items: center;
  gap: 15px;
  background-color: #D2143A; /* Strawberry Red */
  color: #FFF;
  font-family: 'Outfit', sans-serif;
  font-weight: 700;
  font-size: 1.2rem;
  padding: 16px 32px;
  text-decoration: none;
  border: 3px solid #111;
  border-radius: 16px;
  box-shadow: 8px 8px 0px #111;
  transition: all 0.2s ease;
  position: relative;
  z-index: 2;
}

.btn-brutalist:hover {
  transform: translate(-4px, -4px);
  box-shadow: 12px 12px 0px #111;
  background-color: #F4C2C2; /* Zmiana na różowy przy hover */
  color: #111;
}

.btn-brutalist:active {
  transform: translate(4px, 4px);
  box-shadow: 4px 4px 0px #111;
}

.arrow {
  font-size: 1.4rem;
  transition: transform 0.3s ease;
}

.btn-brutalist:hover .arrow {
  transform: translateX(5px);
}

.decor-star {
  position: absolute;
  right: -40px;
  top: -30px;
  font-size: 3rem;
  color: #90EE90;
  text-shadow: 2px 2px 0 #111;
  z-index: 1;
}

/* --- PRAWA STRONA (WIDEO W RAMCE) --- */
.hero-visual {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}

.video-frame {
  position: relative;
  width: 100%;
  aspect-ratio: 4/5; /* Pionowy format a'la Polaroid/Instagram */
  max-width: 500px;
  background: #FFF;
  border: 4px solid #111;
  border-radius: 40px;
  overflow: hidden;
  /* Mega cień w dwóch kolorach z biznesplanu */
  box-shadow: 15px 15px 0px #F4C2C2, 30px 30px 0px #D2143A;
  transform: rotate(3deg);
  transition: transform 0.5s cubic-bezier(0.16, 1, 0.3, 1);
}

.video-frame:hover {
  transform: rotate(0deg) scale(1.02);
}

.hero-video {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.video-overlay {
  position: absolute;
  inset: 0;
  background: rgba(244, 194, 194, 0.2); /* Lekko różowy filtr */
  pointer-events: none;
  z-index: 2;
}

/* RWD - MOBILE */
@media (max-width: 968px) {
  .hero-container {
    grid-template-columns: 1fr;
    gap: 50px;
    text-align: center;
  }
  
  .hero-content {
    align-items: center;
  }
  
  .badge {
    transform: rotate(0);
  }
  
  .title .highlight {
    display: block;
    transform: rotate(0);
    margin-top: 5px;
  }
  
  .subtitle {
    margin: 0 auto 30px;
  }
  
  .video-frame {
    aspect-ratio: 16/9; /* Zmiana na poziom na małych ekranach */
    border-radius: 20px;
    box-shadow: 10px 10px 0px #F4C2C2, 20px 20px 0px #D2143A;
    transform: rotate(0);
  }
  
  .video-frame:hover {
    transform: none;
  }
}
</style>