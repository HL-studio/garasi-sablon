
<script setup lang="ts">
import { computed } from 'vue'

const images = import.meta.glob(
  '@/assets/garasisablon/galeri/*.{jpg,jpeg,png,webp}',
  {
    eager: true,
    query: '?url',
    import: 'default',
  },
) as Record<string, string>

const gallery = Object.entries(images)
  .sort(([a], [b]) => a.localeCompare(b))
  .map(([path, image]) => {
    const filename = path.split('/').pop() ?? ''
    const title = filename.replace(/\.[^.]+$/, '').replace(/_\d+$/, '')

    return {
      title: title
        .replace(/[_-]/g, ' ')
        .replace(/\b\w/g, (letter) => letter.toUpperCase()),
      image,
    }
  })

// Membagi foto menjadi dua baris
const firstRow = computed(( ) => gallery.filter((_, index) => index % 2 === 0))
const secondRow = computed(( ) => gallery.filter((_, index) => index % 2 !== 0))
</script>

<template>
  <section id="galeri" class="gallery">
    <div class="section-container">
      <div class="section-heading">
        <span class="eyebrow">GALERI GARASI SABLON</span>
        <h2>Karya Kami, <span>Inspirasi Kamu.</span></h2>
        <p>
          Lihat berbagai inspirasi kemasan dan hasil visual
          untuk mendukung identitas brand minuman kamu.
        </p>
      </div>
    </div>

    <!-- Baris pertama bergerak ke kiri -->
    <div class="marquee">
      <div class="marquee-track">
        <div
          v-for="(item, index) in [...firstRow, ...firstRow]"
          :key="`first-${index}`"
          class="gallery-card"
        >
          <img
            :src="item.image"
            :alt="item.title"
            loading="lazy"
          />

          <div class="gallery-caption">
            <h3>{{ item.title }}</h3>
          </div>
        </div>
      </div>
    </div>

    <!-- Baris kedua juga bergerak ke kiri dengan kecepatan berbeda -->
    <div class="marquee marquee-reverse">
      <div class="marquee-track">
        <div
          v-for="(item, index) in [...secondRow, ...secondRow]"
          :key="`second-${index}`"
          class="gallery-card"
        >
          <img
            :src="item.image"
            :alt="item.title"
            loading="lazy"
          />

          <div class="gallery-caption">
            <h3>{{ item.title }}</h3>
          </div>
        </div>
      </div>
    </div>

    <div class="section-container">
      <p class="gallery-note">
        Setiap kemasan punya cerita. Wujudkan identitas brand
        minuman kamu bersama Garasi Sablon.
      </p>
    </div>
  </section>
</template>

<style scoped>

</style>
