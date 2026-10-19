
<script setup lang="ts">
import { computed, ref } from 'vue'

const activeCategory = ref('Semua')

const categories = ['Semua', '12 Oz', '14 Oz', '16 Oz']

// Mengambil semua foto katalog secara otomatis
const images = import.meta.glob(
  '/src/assets/garasisablon/katalog/*.{jpg,jpeg,png,webp}',
  {
    eager: true,
    query: '?url',
    import: 'default',
  },
) as Record<string, string>

// Membuat data produk berdasarkan nama file
const products = Object.entries(images)
  .map(([path, image], index) => {
    const filename = path.split('/').pop() ?? ''
    const filenameWithoutExtension = filename.replace(/\.[^.]+$/, '')

    // Mendeteksi kategori dari nama file
    const match = filenameWithoutExtension.match(/^(12|14|16)oz/i)

    if (!match) return null

    const size = match[1]
    const category = `${size} Oz`

    // Mengambil nama warna dari nama file
    const colorName = filenameWithoutExtension
      .replace(/^(12|14|16)oz/i, '')
      .replace(/^$/, 'default')

    const colorLabels: Record<string, string> = {
      default: 'Standar',
      birutua: 'Biru Tua',
      biru: 'Biru',
      hijau: 'Hijau',
      hitam: 'Hitam',
      merah: 'Merah',
      orange: 'Orange',
      pinl: 'Pink',
      pink: 'Pink',
      putih: 'Putih',
      silver: 'Silver',
    }

    const color =
      colorLabels[colorName.toLowerCase()] ??
      colorName.replace(/([a-z])([A-Z])/g, '$1 $2')

    return {
      id: index + 1,
      name:
        colorName.toLowerCase() === 'default'
          ? `Cup Ukuran ${size} Oz`
          : `Cup ${size} Oz ${color}`,
      category,
      size: `${size} oz`,
      price: 'Hubungi kami',
      image,
      color,
    }
  })
  .filter((product) => product !== null)

// Filter produk berdasarkan kategori
const filteredProducts = computed(() => {
  if (activeCategory.value === 'Semua') {
    return products
  }

  return products.filter(
    (product) => product.category === activeCategory.value,
  )
})

// WhatsApp untuk konsultasi produk
function orderProduct(productName: string) {
  const phone = '6281234567890' // Ganti dengan nomor WhatsApp Garasi Sablon

  const message = encodeURIComponent(
    `Halo Garasi Sablon, saya ingin bertanya tentang ${productName}. Mohon informasi harga dan minimum order.`,
  )

  window.open(
    `https://wa.me/${phone}?text=${message}`,
    '_blank',
    'noopener,noreferrer',
  )
}
</script>

<template>
  <section id="katalog" class="catalog section-container">
    <!-- Heading -->
    <div class="section-heading">
      <span class="eyebrow">PILIH PRODUK</span>

      <h2>
        Temukan Cup untuk
        <span>Brand Kamu.</span>
      </h2>

      <p>
        Pilihan produk untuk kebutuhan bisnis minuman,
        promosi, dan identitas brand.
      </p>
    </div>

    <!-- Filter kategori -->
    <div class="catalog-filters">
      <button
        v-for="category in categories"
        :key="category"
        type="button"
        :class="{ active: activeCategory === category }"
        :aria-pressed="activeCategory === category"
        @click="activeCategory = category"
      >
        {{ category }}
      </button>
    </div>

    <!-- Informasi jumlah produk -->
    <div class="catalog-meta">
      <span>
        Menampilkan
        <strong>{{ filteredProducts.length }}</strong>
        produk
      </span>

      <span class="catalog-current">
        Kategori: {{ activeCategory }}
      </span>
    </div>

    <!-- Grid produk -->
    <div v-if="filteredProducts.length" class="product-grid">
      <article
        v-for="product in filteredProducts"
        :key="product.id"
        class="product-card"
      >
        <div class="product-image">
          <img
            :src="product.image"
            :alt="product.name"
            loading="lazy"
          />

          <span class="product-tag">
            {{ product.category }}
          </span>
        </div>

        <div class="product-info">
          <h3>{{ product.name }}</h3>

          <p class="product-size">
            Ukuran {{ product.size }}
          </p>

          <div class="product-bottom">
            <div class="product-price">
              <small>Informasi harga</small>
              <strong>{{ product.price }}</strong>
            </div>

            <button
              class="product-order"
              type="button"
              :aria-label="`Tanya ${product.name} melalui WhatsApp`"
              @click="orderProduct(product.name)"
            >
              <span>↗</span>
            </button>
          </div>
        </div>
      </article>
    </div>

    <!-- Kondisi jika produk kosong -->
    <div v-else class="catalog-empty">
      <h3>Produk belum tersedia</h3>
      <p>
        Belum ada foto untuk kategori ini.
        Silakan pilih kategori lainnya.
      </p>
    </div>

    <!-- Catatan katalog -->
    <div class="catalog-note">
      <span class="note-icon">ⓘ</span>

      <p>
        Harga, minimum order, ukuran, dan ketersediaan produk
        dikonfirmasi saat konsultasi dengan tim Garasi Sablon.
      </p>
    </div>
  </section>
</template>

