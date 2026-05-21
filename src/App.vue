<!-- src/App.vue -->
<template>
  <Navbar />
  <router-view />
  <Footer />
</template>

<script setup>
import Navbar from './components/Navbar.vue';
import Footer from './components/Footer.vue';
</script>

<style>
/* Globalne zmienne i style */
:root {
  --baby-pink: #F4C2C2;
  --strawberry-red: #D2143A;
  --light-green: #90EE90;
  --delicate-yellow: #FFFFE0;
  --white: #FFFFFF;
  --text-dark: #333333;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Poppins', sans-serif;
  background-color: var(--white);
  color: var(--text-dark);
  overflow-x: hidden;
}
</style>