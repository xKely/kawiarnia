<!-- src/components/Navbar.vue -->
<template>
  <header 
    class="navbar-wrapper" 
    :class="{ 'scrolled': isScrolled }" 
    ref="navbarRef"
  >
    <div class="nav-container">
      
      <!-- LOGO -->
      <router-link to="/" class="logo">
        <span class="logo-icon">🍓</span>
        <span class="logo-text">Truskawkowa Rozkosz</span>
      </router-link>

      <!-- LINKI NAWIGACYJNE -->
      <nav class="nav-links">
        <router-link to="/" class="nav-item">Główna</router-link>
        <router-link to="/menu" class="nav-item">Cennik</router-link>
        <router-link to="/about" class="nav-item">O nas</router-link>
      </nav>

      <!-- CALL TO ACTION & MOBILE MENU -->
      <div class="nav-actions">
        <router-link to="/contact" class="btn-contact">
          Kontakt
        </router-link>
        
        <!-- Hamburger Menu na telefony -->
        <button class="menu-toggle" @click="toggleMenu" :class="{ 'active': isMenuOpen }">
          <span class="line"></span>
          <span class="line"></span>
          <span class="line"></span>
        </button>
      </div>

    </div>

    <!-- Wyskakujące Menu Mobilne -->
    <div class="mobile-menu" :class="{ 'open': isMenuOpen }">
      <nav class="mobile-nav-links">
        <router-link to="/" class="mobile-nav-item" @click="closeMenu">Główna</router-link>
        <router-link to="/menu" class="mobile-nav-item" @click="closeMenu">Cennik</router-link>
        <router-link to="/about" class="mobile-nav-item" @click="closeMenu">O nas</router-link>
        <router-link to="/contact" class="mobile-nav-item mobile-btn-contact" @click="closeMenu">Kontakt</router-link>
      </nav>
    </div>
  </header>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import gsap from 'gsap';

const navbarRef = ref(null);
const isScrolled = ref(false);
const isMenuOpen = ref(false);

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50;
};

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};

const closeMenu = () => {
  isMenuOpen.value = false;
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll);

  // Elegancki wjazd z góry
  gsap.fromTo(navbarRef.value, 
    { y: -100, opacity: 0 }, 
    { y: 0, opacity: 1, duration: 0.8, ease: 'power3.out', delay: 0.15 }
  );
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
});
</script>

<style scoped>
/* GŁÓWNY WRAPPER PŁYWAJĄCEGO NAVBARA */
.navbar-wrapper {
  position: fixed;
  top: 25px;
  left: 0;
  right: 0;
  margin: 0 auto; /* Centrowanie bezpieczne dla GSAP */
  width: 95%;
  max-width: 1400px;
  background-color: #FFF;
  border: 4px solid #111;
  border-radius: 24px;
  /* Gruby, brutalistyczny cień - gwarantuje widoczność na każdym tle */
  box-shadow: 8px 8px 0px #111; 
  z-index: 9999;
  /* Zmienione z 'all' na konkretne własności, by nie zakłócać animacji wjazdowej GSAP (transform/opacity) */
  transition: top 0.4s cubic-bezier(0.16, 1, 0.3, 1),
              box-shadow 0.4s cubic-bezier(0.16, 1, 0.3, 1),
              background-color 0.4s cubic-bezier(0.16, 1, 0.3, 1),
              border-color 0.4s cubic-bezier(0.16, 1, 0.3, 1);
  font-family: 'Outfit', sans-serif;
}

/* STAN PO ZESCROLLOWANIU */
.navbar-wrapper.scrolled {
  top: 12px;
  /* Cień zmienia kolor na truskawkowy i robi się lekko mniejszy */
  box-shadow: 6px 6px 0px #D2143A; 
}

.navbar-wrapper.scrolled .nav-container {
  padding: 10px 25px;
}

.nav-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px 30px;
  transition: padding 0.3s ease;
}

/* --- LOGO --- */
.logo {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 1.8rem;
  font-weight: 900;
  color: #111;
  cursor: pointer;
  transition: color 0.3s ease;
  text-decoration: none;
}

.logo-text {
  font-family: 'Pacifico', cursive;
  color: #D2143A;
  letter-spacing: 1px;
}

/* --- LINKI NAWIGACYJNE --- */
.nav-links {
  display: flex;
  gap: 15px;
}

.nav-item {
  text-decoration: none;
  color: #111;
  font-weight: 700;
  font-size: 1.1rem;
  padding: 8px 20px;
  border: 2px solid transparent;
  border-radius: 12px;
  transition: all 0.2s ease;
}

/* Hover na linkach - robi się z nich mały przycisk */
.nav-item:hover, .nav-item.router-link-active {
  background-color: #90EE90; /* Jasna zieleń */
  border: 2px solid #111;
  color: #111 !important;
  box-shadow: 3px 3px 0px #111;
  transform: translateY(-2px);
}

/* --- PRZYCISK KONTAKT (CTA) --- */
.nav-actions {
  display: flex;
  align-items: center;
}

.btn-contact {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 12px 28px;
  font-weight: 800;
  font-size: 1.1rem;
  color: #FFF;
  background-color: #D2143A;
  border: 3px solid #111;
  border-radius: 14px;
  text-decoration: none;
  box-shadow: 4px 4px 0px #111;
  transition: all 0.2s ease;
}

.btn-contact:hover {
  transform: translate(-3px, -3px);
  box-shadow: 7px 7px 0px #111;
  background-color: #F4C2C2; /* Zmiana na różowy przy hover */
  color: #111;
}

.btn-contact:active {
  transform: translate(2px, 2px);
  box-shadow: 2px 2px 0px #111;
}

/* --- HAMBURGER MENU (MOBILE) --- */
.menu-toggle {
  display: none;
  flex-direction: column;
  justify-content: space-between;
  width: 35px;
  height: 25px;
  background: transparent;
  border: none;
  cursor: pointer;
  z-index: 10;
}

.menu-toggle .line {
  display: block;
  width: 100%;
  height: 4px;
  background-color: #111;
  border-radius: 2px;
  transition: all 0.3s ease;
}

/* Animacja hamburgera do X */
.menu-toggle.active .line:nth-child(1) {
  transform: translateY(10px) rotate(45deg);
  background-color: #D2143A !important;
}

.menu-toggle.active .line:nth-child(2) {
  opacity: 0;
}

.menu-toggle.active .line:nth-child(3) {
  transform: translateY(-11px) rotate(-45deg);
  background-color: #D2143A !important;
}

/* --- ROZWIJANE MENU MOBILNE --- */
.mobile-menu {
  position: absolute;
  top: 100%;
  left: -4px;
  right: -4px;
  background-color: #FFFFE0; /* Delicate Yellow */
  border: 4px solid #111;
  border-top: none;
  border-radius: 0 0 24px 24px;
  box-shadow: 8px 8px 0px #111;
  overflow: hidden;
  max-height: 0;
  opacity: 0;
  transform: translateY(-10px);
  transition: max-height 0.4s cubic-bezier(0.16, 1, 0.3, 1),
              opacity 0.3s ease,
              transform 0.4s cubic-bezier(0.16, 1, 0.3, 1);
  z-index: -1;
}

.mobile-menu.open {
  max-height: 400px;
  opacity: 1;
  transform: translateY(0);
}

.mobile-nav-links {
  display: flex;
  flex-direction: column;
  padding: 30px 20px;
  gap: 15px;
}

.mobile-nav-item {
  text-decoration: none;
  color: #111;
  font-weight: 800;
  font-size: 1.4rem;
  padding: 12px 20px;
  border: 2px solid transparent;
  border-radius: 12px;
  text-align: center;
  
  /* Przygotowanie pod animację wejścia (stagger) */
  opacity: 0;
  transform: translateY(15px);
  transition: opacity 0.3s ease, 
              transform 0.3s cubic-bezier(0.16, 1, 0.3, 1), 
              background-color 0.2s ease, 
              border-color 0.2s ease, 
              box-shadow 0.2s ease;
}

/* Kaskadowe opóźnienia linków tylko podczas otwierania */
.mobile-menu.open .mobile-nav-item {
  opacity: 1;
  transform: translateY(0);
}

.mobile-menu.open .mobile-nav-item:nth-child(1) {
  transition-delay: 0.08s;
}
.mobile-menu.open .mobile-nav-item:nth-child(2) {
  transition-delay: 0.15s;
}
.mobile-menu.open .mobile-nav-item:nth-child(3) {
  transition-delay: 0.22s;
}
.mobile-menu.open .mobile-nav-item:nth-child(4) {
  transition-delay: 0.29s;
}

.mobile-menu.open .mobile-nav-item:hover,
.mobile-menu.open .mobile-nav-item.router-link-active {
  background-color: #90EE90; /* Jasna zieleń */
  border: 2px solid #111;
  box-shadow: 4px 4px 0px #111;
  transform: translateY(-2px);
}

.mobile-btn-contact {
  background-color: #D2143A;
  color: #FFF;
  border: 3px solid #111;
  box-shadow: 4px 4px 0px #111;
  transition: background-color 0.2s ease, color 0.2s ease, transform 0.2s ease;
}

.mobile-menu.open .mobile-btn-contact:hover {
  background-color: #F4C2C2;
  color: #111;
  transform: translateY(-2px);
}

/* --- RWD (RESPONSIVE) --- */
@media (max-width: 968px) {
  .nav-links, .btn-contact {
    display: none;
  }
  
  .menu-toggle {
    display: flex;
  }
  
  .nav-container {
    padding: 12px 20px;
    transition: padding 0.3s ease;
  }

  .navbar-wrapper.scrolled .nav-container {
    padding: 8px 16px;
  }
}
</style>