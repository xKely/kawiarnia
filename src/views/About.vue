<!-- src/views/About.vue -->
<template>
  <main class="about-page">
    
    <!-- NAGŁÓWEK -->
    <header class="about-header" ref="headerRef">
      <div class="badge">Za kulisami</div>
      <h1 class="title">Nasza <span class="highlight">Historia</span></h1>
      <p class="subtitle">Jak zrobiliśmy najbardziej kolorowe retro miejsce w Krakowie.</p>
    </header>

    <!-- OŚ CZASU (TIMELINE) -->
    <section class="timeline-section" ref="timelineRef">
      <div class="timeline-line" ref="lineRef"></div>
      
      <div class="timeline-item" v-for="(event, index) in historyData" :key="index" :class="index % 2 === 0 ? 'left' : 'right'">
        <div class="timeline-dot"></div>
        <div class="timeline-content" :style="{ backgroundColor: event.bgColor, boxShadow: `8px 8px 0px ${event.shadowColor}` }">
          <span class="timeline-date">{{ event.date }}</span>
          <h3>{{ event.title }}</h3>
          <p>{{ event.desc }}</p>
        </div>
      </div>
    </section>

    <!-- SEKCJA ZAŁOGI -->
    <section class="team-section" ref="teamRef">
      <h2 class="section-title">Właścicielka <span class="highlight-small pink-highlight">& Załoga</span></h2>
      <p class="section-desc">Ludzie, którzy dbają o słodki klimat lat 60. każdego dnia.</p>
      
      <div class="team-grid">
        <div 
          class="team-card" 
          v-for="(member, index) in teamMembers" 
          :key="index"
        >
          <div class="card-avatar" :style="{ backgroundColor: member.bgColor }">
            <span class="avatar-placeholder">{{ member.emoji }}</span>
          </div>
          <div class="card-info">
            <h3 class="author-name">{{ member.name }}</h3>
            <p class="author-role">{{ member.role }}</p>
            <p class="author-bio">{{ member.bio }}</p>
            <div class="social-tags">
              <span v-for="(tag, i) in member.tags" :key="i">{{ tag }}</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    
    <!-- AKTUALNOŚCI (NEWSBOARD) -->
    <section class="news-section" ref="newsRef">
      <div class="news-board">
        <div class="tape top-left"></div>
        <div class="tape top-right"></div>
        <h2 class="board-title">📌 Tablica Ogłoszeń</h2>
        <ul class="news-list">
          <li><strong>24.05.2026:</strong> W sobotę robimy pokaz Latte Art. Chcesz zobaczyć, jak rysować na mleku? Zapraszamy.</li>
          <li><strong>15.05.2026:</strong> Na młynku nowa Etiopia. Bardzo owocowa, z wyraźnym posmakiem truskawek.</li>
          <li><strong>01.05.2026:</strong> Ogródek letni przed lokalem oficjalnie otwarty. Zapraszamy po dawkę słońca.</li>
        </ul>
      </div>
    </section>

  </main>
</template>
 
<script setup>
import { ref, onMounted } from 'vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);
//ez
// Dane do osi czasu - łatwe w edycji
const historyData = [
  {
    date: "Wiosna 2025",
    title: "Pierwsze plany",
    desc: "Szybka kawa na mieście i pomysł: robimy kawiarnię inspirowaną stylem retro z lat 60. Bez kompromisów.",
    bgColor: "#FFFFE0", // Yellow
    shadowColor: "#111"
  },
  {
    date: "Jesień 2025",
    title: "Wybór lokalu",
    desc: "Znaleźliśmy wolny lokal przy Lema 19 w Nowej Hucie. Świetne światło, dobre sąsiedztwo i idealny metraż pod nasz pomysł.",
    bgColor: "#F4C2C2", // Pink
    shadowColor: "#D2143A" // Red
  },
  {
    date: "Zima 2025",
    title: "Tutaj zaczęła się nasza przygoda",
    desc: "Zakup mebli i wyposażenia itp.",
    bgColor: "#90EE90", // Green
    shadowColor: "#111"
  },
  {
    date: "Maj 2026",
    title: "Otwieramy drzwi!",
    desc: "Ekspres ruszył, a z głośników poleciały klasyki z winyli. Truskawkowa Rozkosz oficjalnie przywitała pierwszych gości.",
    bgColor: "#D2143A", // Red
    shadowColor: "#111"
  }
];

const teamMembers = [
  {
    name: "Aleksandra",
    role: "Właścicielka",
    emoji: "😎",
    bgColor: "#F4C2C2",
    bio: "Założycielka i szefowa całego zamieszania. Pilnuje, żeby ziarna zawsze były świeże, a z głośników leciał dobry rock'n'roll.",
    tags: ["#Właścicielka", "#Lata60", "#Kawa"]
  },
  {
    name: "Katarzyna",
    role: "Menadżerka",
    emoji: "☕",
    bgColor: "#90EE90",
    bio: "Jest mózgiem i sercem operacyjnym kawiarni. Odpowiada za finanse, grafiki i dbanie o to, żeby obsługa wiedziała co ma robić.",
    tags: ["#Menadżerka", "#LatteArt", "#Kofeina"]
  },
  {
    name: "Patryk",
    role: "Kelner",
    emoji: "🍰",
    bgColor: "#FFFFE0",
    bio: "W naszej obsłudze trzymamy poziom. Patryk ogarnie Wasze zamówienie, doradzi ciasto i zawsze znajdzie dobre słowo.",
    tags: ["#Kelner", "#Uśmiech", "#Lata60"]
  },
  {
    name: "Maks",
    role: "Barista",
    emoji: "👨‍🍳",
    bgColor: "#F4C2C2",
    bio: "Specjalista od mleka i ziaren. Potrafi wyczarować idealne Truskawcino o każdej porze dnia. Zawsze chętny do rozmowy o kawie.",
    tags: ["#Barista", "#Kofeina", "#LatteArt"]
  },
  {
    name: "Vika",
    role: "Marketing",
    emoji: "📊",
    bgColor: "#FFFFE0",
    bio: "Za monitorem i telefonem. Odpowiada za relacje z Wami w sieci, social media i pilnuje, żeby media społecznościowe wyglądały tak dobrze, jak nasza kawa.",
    tags: ["#Marketing", "#Kofeina", "#LatteArt"]
  }
];

const headerRef = ref(null);
const timelineRef = ref(null);
const lineRef = ref(null);
const teamRef = ref(null);
const zonesRef = ref(null);
const newsRef = ref(null);

onMounted(() => {
  // 1. Animacja nagłówka (wjazd)
  gsap.fromTo(headerRef.value.children,
    { y: 40, opacity: 0 },
    { y: 0, opacity: 1, duration: 0.8, stagger: 0.15, ease: 'back.out(1.5)', delay: 0.2 }
  );

  // 2. Animacja Osi Czasu (rysowanie linii z góry na dół)
  gsap.fromTo(lineRef.value,
    { height: "0%" },
    {
      height: "100%",
      ease: "none",
      scrollTrigger: {
        trigger: timelineRef.value,
        start: "top 60%",
        end: "bottom 80%",
        scrub: true
      }
    }
  );

  // 3. Wjazd poszczególnych okienek z historią (z lewej lub z prawej)
  const timelineItems = gsap.utils.toArray('.timeline-item');
  timelineItems.forEach((item, i) => {
    const isLeft = i % 2 === 0;
    gsap.fromTo(item.querySelector('.timeline-content'),
      { x: isLeft ? -100 : 100, opacity: 0, rotation: isLeft ? -5 : 5 },
      {
        x: 0, opacity: 1, rotation: 0, duration: 0.8, ease: 'back.out(1.2)',
        scrollTrigger: {
          trigger: item,
          start: "top 85%"
        }
      }
    );
    // Pojawianie się kropek na osi
    gsap.fromTo(item.querySelector('.timeline-dot'),
      { scale: 0 },
      { scale: 1, duration: 0.5, ease: 'back.out(2)', scrollTrigger: { trigger: item, start: "top 85%" } }
    );
  });

  // 4. Karty autorów/teamu
  gsap.fromTo(".team-card",
    { y: 80, opacity: 0, rotation: 3 },
    {
      y: 0, opacity: 1, rotation: 0, duration: 0.8, stagger: 0.2, ease: 'back.out(1.2)',
      scrollTrigger: { trigger: teamRef.value, start: "top 80%" }
    }
  );

  // 5. Karty stref
  gsap.fromTo(".zone-card",
    { y: 60, opacity: 0, rotation: -2 },
    {
      y: 0, opacity: 1, rotation: 0, duration: 0.8, stagger: 0.15, ease: 'back.out(1.2)',
      scrollTrigger: { trigger: ".zones-grid", start: "top 85%" }
    }
  );

  // 6. Tablica Ogłoszeń (wskakuje z dołu)
  gsap.fromTo(".news-board",
    { y: 100, opacity: 0, rotation: -2 },
    {
      y: 0, opacity: 1, rotation: 2, duration: 0.8, ease: 'back.out(1.5)',
      scrollTrigger: { trigger: newsRef.value, start: "top 90%" }
    }
  );
});
</script>

<style scoped>
.about-page {
  min-height: 100vh;
  padding: 150px 5vw 100px;
  background-color: #FAFAFA;
  font-family: 'Outfit', sans-serif;
  overflow-x: hidden;
}

/* --- NAGŁÓWEK --- */
.about-header {
  text-align: center;
  max-width: 800px;
  margin: 0 auto 80px;
}

.badge {
  display: inline-block;
  font-weight: 800;
  color: #111;
  background-color: #90EE90; /* Light green */
  padding: 8px 24px;
  border: 3px solid #111;
  border-radius: 50px;
  text-transform: uppercase;
  margin-bottom: 20px;
  box-shadow: 4px 4px 0px #111;
  transform: rotate(2deg);
}

.title {
  font-size: clamp(3rem, 7vw, 5rem);
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

/* --- OŚ CZASU (TIMELINE) --- */
.timeline-section {
  position: relative;
  max-width: 1000px;
  margin: 0 auto 120px;
  padding: 40px 0;
}

/* Główna linia idąca przez środek */
.timeline-line {
  position: absolute;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 6px;
  background-color: #111;
  border-radius: 6px;
  z-index: 1;
}

.timeline-item {
  display: flex;
  justify-content: flex-end;
  padding-right: 50%;
  position: relative;
  margin-bottom: 60px;
  width: 100%;
}

.timeline-item.right {
  justify-content: flex-start;
  padding-right: 0;
  padding-left: 50%;
}

/* Kropka na osi */
.timeline-dot {
  position: absolute;
  top: 20px;
  left: 50%;
  transform: translate(-50%, 0);
  width: 24px;
  height: 24px;
  background-color: #FFF;
  border: 5px solid #D2143A;
  border-radius: 50%;
  z-index: 2;
  box-shadow: 0 0 0 4px #111;
}

/* Pudełko z treścią */
.timeline-content {
  width: 85%;
  border: 4px solid #111;
  border-radius: 16px;
  padding: 25px;
  position: relative;
  z-index: 3;
}

.timeline-item.left .timeline-content {
  margin-right: 40px;
}

.timeline-item.right .timeline-content {
  margin-left: 40px;
}

.timeline-date {
  display: inline-block;
  background-color: #111;
  color: #FFF;
  font-weight: 800;
  padding: 4px 12px;
  border-radius: 20px;
  margin-bottom: 15px;
  font-size: 0.9rem;
}

.timeline-content h3 {
  font-size: 1.8rem;
  font-weight: 900;
  color: #111;
  margin-bottom: 10px;
}

.timeline-content p {
  font-size: 1.05rem;
  font-weight: 500;
  color: #222;
  line-height: 1.5;
}

/* --- AUTORZY PROJEKTU --- */
.team-section {
  max-width: 1200px;
  margin: 0 auto 120px;
  text-align: center;
}

.section-title {
  font-size: 3rem;
  font-weight: 900;
  color: #111;
  text-transform: uppercase;
  margin-bottom: 10px;
}

.highlight-small {
  font-family: 'Pacifico', cursive;
  text-shadow: 2px 2px 0px #111;
  text-transform: none;
}

.pink-highlight {
  color: #F4C2C2;
}

.green-highlight {
  color: #90EE90 !important;
}

.section-desc {
  font-size: 1.2rem;
  color: #444;
  margin-bottom: 50px;
}

.team-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 40px;
  justify-content: center;
}

.team-card {
  width: 100%;
  max-width: 420px;
  background: #FFF;
  border: 4px solid #111;
  border-radius: 20px;
  padding: 40px 20px;
  box-shadow: 12px 12px 0px #F4C2C2;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  justify-self: center;
}

.team-card:hover {
  transform: translate(-5px, -5px) !important;
  box-shadow: 16px 16px 0px #D2143A;
}

.card-avatar {
  width: 120px;
  height: 120px;
  margin: 0 auto 20px;
  border: 4px solid #111;
  border-radius: 50%;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 4px 4px 0px #111;
}

.avatar-placeholder {
  font-size: 4rem;
}

.author-name {
  font-size: 1.8rem;
  font-weight: 900;
  color: #111;
  margin-bottom: 5px;
}

.author-role {
  font-size: 1rem;
  font-weight: 700;
  color: #D2143A;
  margin-bottom: 12px;
  text-transform: uppercase;
}

.author-bio {
  font-size: 1rem;
  color: #444;
  line-height: 1.5;
  margin-bottom: 20px;
  padding: 0 15px;
}

.social-tags {
  display: flex;
  justify-content: center;
  gap: 10px;
  flex-wrap: wrap;
}

.social-tags span {
  background-color: #FFFFE0;
  border: 2px solid #111;
  padding: 4px 10px;
  border-radius: 10px;
  font-size: 0.85rem;
  font-weight: 700;
  box-shadow: 2px 2px 0px #111;
}

/* --- SEKCJA STREF W LOKALU --- */
.zones-section {
  max-width: 1200px;
  margin: 0 auto 120px;
  text-align: center;
}

.zones-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 30px;
  justify-content: center;
}

.zone-card {
  width: 100%;
  max-width: 380px;
  border: 4px solid #111;
  border-radius: 20px;
  padding: 35px 25px;
  text-align: left;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  justify-self: center;
}

.zone-card:hover {
  transform: translate(-4px, -4px) !important;
  box-shadow: 12px 12px 0px #111 !important;
}

.zone-icon {
  font-size: 3rem;
  display: inline-block;
  margin-bottom: 15px;
  filter: drop-shadow(2px 2px 0px rgba(0,0,0,0.15));
}

.zone-card h3 {
  font-size: 1.5rem;
  font-weight: 900;
  color: #111;
  margin-bottom: 10px;
  text-transform: uppercase;
}

.zone-card p {
  font-size: 1rem;
  font-weight: 500;
  color: #333;
  line-height: 1.5;
}

/* Kolory stref */
.pink-card {
  background-color: #F4C2C2;
  box-shadow: 8px 8px 0px #111;
}

.green-card {
  background-color: #90EE90;
  box-shadow: 8px 8px 0px #111;
}

.yellow-card {
  background-color: #FFFFE0;
  box-shadow: 8px 8px 0px #111;
}

/* --- TABLICA OGŁOSZEŃ (AKTUALNOŚCI) --- */
.news-section {
  max-width: 800px;
  margin: 0 auto;
}

.news-board {
  background-color: #FFFFE0;
  border: 4px solid #111;
  border-radius: 8px;
  padding: 40px;
  position: relative;
  box-shadow: 10px 10px 0px #111;
  transform: rotate(2deg);
}

.tape {
  position: absolute;
  width: 100px;
  height: 30px;
  background-color: rgba(255, 255, 255, 0.6);
  border: 1px solid #CCC;
  box-shadow: 1px 1px 3px rgba(0,0,0,0.1);
  z-index: 10;
}

.top-left {
  top: -15px;
  left: -20px;
  transform: rotate(-30deg);
}

.top-right {
  top: -15px;
  right: -20px;
  transform: rotate(25deg);
}

.board-title {
  font-family: 'Pacifico', cursive;
  font-size: 2.5rem;
  color: #D2143A;
  text-align: center;
  margin-bottom: 30px;
}

.news-list {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.news-list li {
  font-size: 1.15rem;
  font-weight: 500;
  color: #333;
  line-height: 1.5;
  padding-bottom: 15px;
  border-bottom: 2px dashed #111;
}

.news-list li:last-child {
  border-bottom: none;
}

/* RWD - MOBILE */
@media (max-width: 768px) {
  /* Oś czasu na komórkach układa się z jednej strony */
  .timeline-line {
    left: 20px;
  }
  
  .timeline-item {
    justify-content: flex-start;
    padding-right: 0;
    padding-left: 50px; /* Miejsce na linię po lewej */
  }
  
  .timeline-item.right {
    padding-left: 50px;
  }

  .timeline-dot {
    left: 20px;
  }

  .timeline-item.left .timeline-content,
  .timeline-item.right .timeline-content {
    width: 100%;
    margin-left: 0;
    margin-right: 0;
  }
  
  .news-board {
    transform: rotate(0);
    padding: 30px 20px;
  }
}
</style>