<!-- src/components/Footer.vue -->
<template>
  <footer class="footer-neo" ref="footerRef">
    
    <!-- RETRO PASEK INFORMACYJNY (TICKER TAPE) -->
    <div class="ticker-wrap">
      <div class="ticker-move">
        <div class="ticker-item">🍓 SŁODKIE CHWILE W RYTMIE LAT 60.</div>
        <div class="ticker-item">✦</div>
        <div class="ticker-item">WŁASNY WYPAŁ ZIAREN</div>
        <div class="ticker-item">✦</div>
        <div class="ticker-item">CODZIENNIE ŚWIEŻE CIASTA</div>
        <div class="ticker-item">✦</div>
        <!-- Duplikaty dla nieskończonego efektu -->
        <div class="ticker-item">🍓 SŁODKIE CHWILE W RYTMIE LAT 60.</div>
        <div class="ticker-item">✦</div>
        <div class="ticker-item">WŁASNY WYPAŁ ZIAREN</div>
        <div class="ticker-item">✦</div>
        <div class="ticker-item">CODZIENNIE ŚWIEŻE CIASTA</div>
        <div class="ticker-item">✦</div>
      </div>
    </div>

    <!-- GŁÓWNA ZAWARTOŚĆ STOPKI -->
    <div class="footer-container">
      
      <!-- Kolumna 1: Marka i Social Media -->
      <div class="footer-col brand-col" ref="col1Ref">
        <h3 class="footer-logo">Truskawkowa<br>Rozkosz</h3>
        <p class="brand-desc">
          Autorska kawiarnia w Krakowie. Dobre espresso, domowe desery i retro klimat lat 60.
        </p>
      </div>

      <!-- Kolumna 2: Karta z godzinami -->
      <div class="footer-col" ref="col2Ref">
        <div class="info-card pink-card">
          <h4 class="card-title">Godziny otwarcia</h4>
          <p class="card-text">
            Poniedziałek - Niedziela<br>
            <span class="highlight-text">6:00 - 17:00</span>
          </p>
        </div>
      </div>

      <!-- Kolumna 3: Karta z adresem -->
      <div class="footer-col" ref="col3Ref">
        <div class="info-card green-card">
          <h4 class="card-title">Gdzie jesteśmy?</h4>
          <p class="card-text">
            ul. Stanisława Lema 19<br>
            <span class="highlight-text">Kraków</span>
          </p>
        </div>
      </div>



    </div>

    <!-- DOLNY PASEK COPYRIGHT -->
    <div class="footer-bottom">
      <p>&copy; 2026 Truskawkowa Rozkosz. Wszelkie prawa zastrzeżone.</p>
      <div class="bottom-links">
        <a href="#">Regulamin</a>
        <a href="#">Polityka Prywatności</a>
      </div>
    </div>

  </footer>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

const footerRef = ref(null);
const col1Ref = ref(null);
const col2Ref = ref(null);
const col3Ref = ref(null);
const col4Ref = ref(null);

onMounted(() => {
  // Animacja wjazdu kolumn stopki po zescrollowaniu
  gsap.fromTo(
    [col1Ref.value, col2Ref.value, col3Ref.value, col4Ref.value],
    { y: 60, opacity: 0 },
    {
      y: 0, 
      opacity: 1, 
      duration: 0.8, 
      stagger: 0.15, 
      ease: 'back.out(1.2)',
      scrollTrigger: {
        trigger: footerRef.value,
        start: "top 85%", // Odpala, gdy top stopki wejdzie na 85% wysokości ekranu
      }
    }
  );
});

// Mikro-interakcja dla newslettera
const handleSubscribe = (e) => {
  const btn = e.target.querySelector('button');
  const originalText = btn.innerText;
  
  gsap.to(btn, { scale: 0.95, duration: 0.1, yoyo: true, repeat: 1 });
  
  btn.innerText = "Zapisano! 🎉";
  btn.style.backgroundColor = "#90EE90"; // Jasna zieleń z biznesplanu
  
  setTimeout(() => {
    btn.innerText = originalText;
    btn.style.backgroundColor = "#FFFFE0"; // Powrót do żółtego
    e.target.reset();
  }, 3000);
};
</script>

<style scoped>
/* GŁÓWNA STOPKA (CIEMNE TŁO DLA KONTRASTU) */
.footer-neo {
  background-color: #111;
  color: #FFF;
  font-family: 'Outfit', sans-serif;
  overflow: hidden;
  border-top: 6px solid #111;
  position: relative;
  z-index: 10;
}

/* --- TICKER TAPE (PŁYWAJĄCY TEKST) --- */
.ticker-wrap {
  width: 100%;
  overflow: hidden;
  background-color: #FFFFE0; /* Delicate Yellow */
  border-bottom: 4px solid #111;
  padding: 12px 0;
  display: flex;
  white-space: nowrap;
}

.ticker-move {
  display: flex;
  animation: ticker 15s linear infinite;
}

.ticker-item {
  font-family: 'Outfit', sans-serif;
  font-weight: 900;
  font-size: 1.2rem;
  color: #111;
  padding: 0 20px;
  text-transform: uppercase;
  letter-spacing: 2px;
}

@keyframes ticker {
  0% { transform: translate3d(0, 0, 0); }
  100% { transform: translate3d(-50%, 0, 0); } /* Przesuwa się dokładnie o połowę długości by pętla była idealna */
}

/* --- KONTENER I KOLUMNY --- */
.footer-container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 80px 5vw;
  display: grid;
  grid-template-columns: 2fr 1fr 1fr 1.5fr;
  gap: 50px;
}

/* KOLUMNA 1: LOGO */
.footer-logo {
  font-family: 'Pacifico', cursive;
  font-size: 2.5rem;
  color: #D2143A; /* Strawberry Red */
  line-height: 1.2;
  margin-bottom: 20px;
  text-shadow: 2px 2px 0px #FFF; /* Retro biały cień na czarnym tle */
  transform: rotate(-2deg);
}

.brand-desc {
  font-size: 1.05rem;
  line-height: 1.6;
  color: #CCC;
  margin-bottom: 30px;
  max-width: 90%;
}

.socials {
  display: flex;
  gap: 15px;
}

.social-btn {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 50px;
  height: 50px;
  background-color: #FFF;
  color: #111;
  font-weight: 800;
  text-decoration: none;
  border: 3px solid #111;
  border-radius: 50%;
  box-shadow: 4px 4px 0px #D2143A;
  transition: all 0.2s ease;
}

.social-btn:hover {
  transform: translate(-3px, -3px);
  box-shadow: 7px 7px 0px #D2143A;
  background-color: #F4C2C2;
}

/* BRUTALISTYCZNE KARTY (KOLUMNA 2 i 3) */
.info-card {
  padding: 25px 20px;
  border: 3px solid #111;
  border-radius: 16px;
  color: #111;
  transform: rotate(2deg);
  transition: transform 0.3s ease;
}

.info-card:hover {
  transform: rotate(0deg) scale(1.02);
}

.pink-card {
  background-color: #F4C2C2;
  box-shadow: 6px 6px 0px #FFF;
}

.green-card {
  background-color: #90EE90;
  box-shadow: 6px 6px 0px #FFF;
  transform: rotate(-2deg);
}

.card-title {
  font-size: 1.1rem;
  font-weight: 800;
  margin-bottom: 15px;
  text-transform: uppercase;
  border-bottom: 2px solid #111;
  padding-bottom: 8px;
}

.card-text {
  font-size: 1rem;
  line-height: 1.6;
  font-weight: 500;
}

.highlight-text {
  font-size: 1.2rem;
  font-weight: 800;
  display: block;
  margin-top: 5px;
}

/* KOLUMNA 4: NEWSLETTER */
.newsletter-title {
  font-size: 1.8rem;
  font-weight: 800;
  color: #FFFFE0;
  margin-bottom: 15px;
}

.newsletter-desc {
  font-size: 1rem;
  color: #CCC;
  margin-bottom: 25px;
  line-height: 1.5;
}

.newsletter-form {
  display: flex;
  gap: 10px;
}

.newsletter-form input {
  flex: 1;
  padding: 15px;
  font-family: 'Outfit', sans-serif;
  font-size: 1rem;
  border: 3px solid #111;
  border-radius: 12px;
  outline: none;
  background: #FFF;
}

.newsletter-form input:focus {
  box-shadow: 4px 4px 0px #F4C2C2;
}

.newsletter-form button {
  padding: 0 25px;
  font-family: 'Outfit', sans-serif;
  font-weight: 800;
  font-size: 1.1rem;
  background-color: #FFFFE0;
  color: #111;
  border: 3px solid #111;
  border-radius: 12px;
  cursor: pointer;
  box-shadow: 4px 4px 0px #D2143A;
  transition: all 0.2s ease;
}

.newsletter-form button:hover {
  transform: translate(-2px, -2px);
  box-shadow: 6px 6px 0px #D2143A;
}

/* DOLNY PASEK COPYRIGHT */
.footer-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 25px 5vw;
  border-top: 2px solid rgba(255, 255, 255, 0.1);
  font-size: 0.9rem;
  color: #888;
}

.bottom-links {
  display: flex;
  gap: 20px;
}

.bottom-links a {
  color: #888;
  text-decoration: none;
  transition: color 0.3s ease;
}

.bottom-links a:hover {
  color: #F4C2C2;
}

/* RWD - MOBILE */
@media (max-width: 1024px) {
  .footer-container {
    grid-template-columns: 1fr 1fr;
  }
}

@media (max-width: 768px) {
  .footer-container {
    grid-template-columns: 1fr;
    gap: 40px;
    padding: 60px 5vw;
  }
  
  .newsletter-form {
    flex-direction: column;
  }
  
  .newsletter-form button {
    padding: 15px;
  }
  
  .footer-bottom {
    flex-direction: column;
    gap: 15px;
    text-align: center;
  }
  
  .info-card {
    transform: rotate(0deg);
  }
}
</style>