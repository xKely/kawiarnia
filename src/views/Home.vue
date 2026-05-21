<!-- src/views/Home.vue -->
<template>
  <main>
    <Hero />
    <Showcase />
    <Gallery />
  </main>
</template>

<script setup>
import Hero from '../components/Hero.vue';
import Showcase from '../components/Showcase.vue';
import Gallery from '../components/Gallery.vue';
</script>