<script setup lang="ts">
import Navbar from './components/Navbar.vue'
import HeroSection from './components/HeroSection.vue'
import CatalogSection from './components/CatalogSection.vue'
import AboutSection from './components/AboutSection.vue'
import BenefitsSection from './components/BenefitsSection.vue'
import ProcessSection from './components/ProcessSection.vue'
import GallerySection from './components/GallerySection.vue'
import FooterSection from './components/FooterSection.vue'
</script>

<template>
  <div class="website">
    <Navbar />

    <main>
      <HeroSection />
      <CatalogSection />
      <AboutSection />
      <BenefitsSection />
      <ProcessSection />
      <GallerySection />
    </main>

    <FooterSection />
  </div>
</template>

<style>
@import './assets/styles.css';
</style>
