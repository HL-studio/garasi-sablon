
<script setup lang="ts">
const benefits = [
  {
    number: '01',
    title: 'Desain Custom',
    description: 'Sesuaikan tampilan cup dengan identitas brand.',
    icon: '✳',
  },
  {
    number: '02',
    title: 'Pilihan Produk',
    description: 'Pilih jenis dan ukuran sesuai kebutuhan.',
    icon: '◈',
  },
  {
    number: '03',
    title: 'Konsultasi Mudah',
    description: 'Diskusikan spesifikasi dan anggaran sebelum order.',
    icon: '↗',
  },
  {
    number: '04',
    title: 'Untuk Berbagai Bisnis',
    description: 'Cocok untuk coffee shop, usaha minuman, dan event.',
    icon: '◎',
  },
]
</script>

<template>
  <section class="benefits">
    <div class="section-container">
      <div class="section-heading">
        <span class="eyebrow">KENAPA GARASI SABLON?</span>
        <h2>Packaging yang Bekerja untuk <span>Brand Kamu.</span></h2>
      </div>

      <div class="benefit-grid">
        <article
          v-for="item in benefits"
          :key="item.number"
          class="benefit-card"
        >
          <div class="benefit-top">
            <span class="benefit-icon">{{ item.icon }}</span>
            <span class="benefit-number">{{ item.number }}</span>
          </div>

          <h3>{{ item.title }}</h3>
          <p>{{ item.description }}</p>
        </article>
      </div>
    </div>
  </section>
</template>
