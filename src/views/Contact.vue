<!-- src/views/Contact.vue -->
<template>
  <main class="contact-page">
    
    <!-- NAGŁÓWEK -->
    <header class="contact-header" ref="headerRef">
      <div class="badge">Napisz do nas</div>
      <h1 class="title">Zostańmy w <span class="highlight">Kontakcie</span></h1>
      <p class="subtitle">Chcesz zarezerwować stolik albo o coś zapytać? Śmiało napisz lub zadzwoń.</p>
    </header>

    <div class="contact-container" ref="containerRef">
      
      <!-- LEWA STRONA: FORMULARZ -->
      <div class="form-card" ref="formRef">
        <form @submit.prevent="handleSubmit" class="contact-form">
          <div class="form-group">
            <label for="name">Imię i nazwisko</label>
            <input type="text" id="name" v-model="form.name" required placeholder="np. Anna Kowalska" />
          </div>

          <div class="form-group">
            <label for="email">Adres E-mail</label>
            <input type="email" id="email" v-model="form.email" required placeholder="np. anna@gmail.com" />
          </div>

          <div class="form-group">
            <label for="message">Wiadomość</label>
            <textarea id="message" v-model="form.message" rows="5" required placeholder="Wpisz treść wiadomości..."></textarea>
          </div>

          <button type="submit" class="btn-submit">
            Wyślij wiadomość 🍓
            <span class="btn-bg"></span>
          </button>
        </form>
      </div>

      <!-- PRAWA STRONA: BLOKI INFORMACYJNE -->
      <div class="info-side" ref="infoRef">
        
        <div class="info-card pink-card">
          <span class="info-icon">📍</span>
          <div>
            <h3>Nasza Lokalizacja</h3>
            <p>ul. Stanisława Lema 19, Kraków</p>
          </div>
        </div>

        <div class="info-card green-card">
          <span class="info-icon">📞</span>
          <div>
            <h3>Zadzwoń do nas</h3>
            <p>+48 123 456 789</p>
          </div>
        </div>

        <div class="info-card yellow-card">
          <span class="info-icon">📧</span>
          <div>
            <h3>Napisz e-mail</h3>
            <p>kontakt@truskawkowarozkosz.pl</p>
          </div>
        </div>

        <div class="info-card pink-card">
          <span class="info-icon">🕒</span>
          <div>
            <h3>Godziny otwarcia</h3>
            <p>Codziennie: 6:00 - 17:00</p>
          </div>
        </div>

      </div>

    </div>

    <!-- Ozobne gwiazdki pop-art -->
    <div class="decor-star star-1">✦</div>
    <div class="decor-star star-2">✦</div>

  </main>
</template>

<script setup>
import { ref, reactive, onMounted } from 'vue';
import gsap from 'gsap';

const form = reactive({
  name: '',
  email: '',
  message: ''
});

const headerRef = ref(null);
const containerRef = ref(null);
const formRef = ref(null);
const infoRef = ref(null);

onMounted(() => {
  // Wjazd nagłówka
  if (headerRef.value) {
    gsap.fromTo(headerRef.value.children,
      { y: 40, opacity: 0 },
      { y: 0, opacity: 1, duration: 0.8, stagger: 0.15, ease: 'back.out(1.5)', delay: 0.2 }
    );
  }

  // Wjazd formularza i info kart
  if (formRef.value) {
    gsap.fromTo(formRef.value,
      { x: -50, opacity: 0 },
      { x: 0, opacity: 1, duration: 0.8, ease: 'back.out(1.2)', delay: 0.4 }
    );
  }

  if (infoRef.value) {
    gsap.fromTo(infoRef.value.children,
      { x: 50, opacity: 0, rotation: () => gsap.utils.random(-5, 5) },
      { x: 0, opacity: 1, rotation: 0, duration: 0.6, stagger: 0.1, ease: 'back.out(1.2)', delay: 0.4 }
    );
  }
});

const handleSubmit = () => {
  alert(`Dziękujemy ${form.name}! Twoja wiadomość została wysłana.`);
  form.name = '';
  form.email = '';
  form.message = '';
};
</script>

<style scoped>
.contact-page {
  min-height: 100vh;
  padding: 150px 5vw 100px;
  background-color: #FAFAFA;
  background-image: radial-gradient(#DDD 1px, transparent 1px);
  background-size: 20px 20px;
  font-family: 'Outfit', sans-serif;
  position: relative;
  overflow: hidden;
}

/* --- NAGŁÓWEK --- */
.contact-header {
  text-align: center;
  max-width: 800px;
  margin: 0 auto 80px;
  position: relative;
  z-index: 10;
}

.badge {
  display: inline-block;
  font-weight: 800;
  color: #111;
  background-color: #90EE90; /* Light Green */
  padding: 8px 24px;
  border: 3px solid #111;
  border-radius: 50px;
  text-transform: uppercase;
  margin-bottom: 20px;
  box-shadow: 4px 4px 0px #111;
  transform: rotate(2deg);
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
  display: inline-block;
  text-shadow: 4px 4px 0px #111;
  transform: rotate(-3deg);
}

.subtitle {
  font-size: 1.25rem;
  font-weight: 500;
  color: #444;
}

/* --- UKŁAD FORMULARZ + INFO --- */
.contact-container {
  max-width: 1100px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1.2fr 0.8fr;
  gap: 50px;
  position: relative;
  z-index: 10;
}

/* --- FORMULARZ --- */
.form-card {
  background-color: #FFF;
  border: 4px solid #111;
  border-radius: 24px;
  padding: 40px;
  box-shadow: 10px 10px 0px #111;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 25px;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 8px;
  text-align: left;
}

.form-group label {
  font-weight: 800;
  color: #111;
  text-transform: uppercase;
  font-size: 0.9rem;
  letter-spacing: 1px;
}

.form-group input,
.form-group textarea {
  padding: 15px;
  font-family: 'Outfit', sans-serif;
  font-size: 1rem;
  border: 3px solid #111;
  border-radius: 12px;
  background-color: #FAFAFA;
  outline: none;
  transition: all 0.3s ease;
}

.form-group input:focus,
.form-group textarea:focus {
  background-color: #FFF;
  box-shadow: 4px 4px 0px #F4C2C2;
}

.btn-submit {
  align-self: flex-start;
  padding: 15px 35px;
  font-family: 'Outfit', sans-serif;
  font-weight: 800;
  font-size: 1.1rem;
  color: #FFF;
  background-color: #D2143A;
  border: 3px solid #111;
  border-radius: 14px;
  cursor: pointer;
  box-shadow: 4px 4px 0px #111;
  transition: all 0.2s ease;
}

.btn-submit:hover {
  transform: translate(-3px, -3px);
  box-shadow: 7px 7px 0px #111;
  background-color: #F4C2C2;
  color: #111;
}

.btn-submit:active {
  transform: translate(2px, 2px);
  box-shadow: 2px 2px 0px #111;
}

/* --- INFO KARTY --- */
.info-side {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.info-card {
  display: flex;
  align-items: center;
  gap: 20px;
  padding: 20px;
  border: 3px solid #111;
  border-radius: 16px;
  color: #111;
  text-align: left;
}

.info-icon {
  font-size: 2.5rem;
  filter: drop-shadow(2px 2px 0 rgba(0,0,0,0.1));
}

.info-card h3 {
  font-size: 1.1rem;
  font-weight: 800;
  text-transform: uppercase;
  margin-bottom: 5px;
}

.info-card p {
  font-size: 1rem;
  font-weight: 500;
}

/* Kolory brutalistycznych kart */
.pink-card {
  background-color: #F4C2C2;
  box-shadow: 6px 6px 0px #111;
}

.green-card {
  background-color: #90EE90;
  box-shadow: 6px 6px 0px #111;
}

.yellow-card {
  background-color: #FFFFE0;
  box-shadow: 6px 6px 0px #111;
}

/* --- DEKORACYJNE GWIAZDKI --- */
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
  top: 10%;
  left: 5%;
  color: #F4C2C2;
  transform: rotate(-15deg);
}

.star-2 {
  bottom: 10%;
  right: 5%;
  transform: rotate(10deg);
}

/* RWD - MOBILE */
@media (max-width: 768px) {
  .contact-container {
    grid-template-columns: 1fr;
    gap: 40px;
  }
  
  .form-card {
    padding: 25px 20px;
  }
  
  .btn-submit {
    width: 100%;
    text-align: center;
  }
}
</style>