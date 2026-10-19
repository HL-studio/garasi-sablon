
<script setup lang="ts">
const steps = [
  { number: '01', title: 'Pilih Produk', desc: 'Tentukan jenis dan ukuran cup.' },
  { number: '02', title: 'Konsultasi', desc: 'Diskusikan desain, jumlah, dan anggaran.' },
  { number: '03', title: 'Konfirmasi', desc: 'Setujui detail dan penawaran pesanan.' },
  { number: '04', title: 'Produksi', desc: 'Pesanan diproses sesuai kesepakatan.' },
]
</script>

<template>
  <section id="proses" class="process section-container">
    <div class="section-heading">
      <span class="eyebrow">MUDAH DAN PRAKTIS</span>
      <h2>Dari Ide Sampai <span>Siap Diproduksi.</span></h2>
      <p>Empat langkah untuk memulai pesanan cup custom kamu.</p>
    </div>

    <div class="process-grid">
      <article v-for="step in steps" :key="step.number" class="process-card">
        <span class="process-number">{{ step.number }}</span>
        <h3>{{ step.title }}</h3>
        <p>{{ step.desc }}</p>
      </article>
    </div>
  </section>
</template>
