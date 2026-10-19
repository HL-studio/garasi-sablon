<script setup lang="ts">
import { ref } from 'vue'

const menuOpen = ref(false)

const closeMenu = () => {
  menuOpen.value = false
}
</script>

<template>
  <header class="navbar">
    <a href="#beranda" class="brand" @click="closeMenu">
      <header class="navbar">
        <a href="#beranda" class="brand" @click="closeMenu">
          <img src="@/assets/garasisablon/logo.png" alt="Logo Garasi Sablon" class="brand-logo" style="background-color:white; border-radius: 20px;"/>
        </a>
      </header>
    </a>

    <button class="menu-toggle" @click="menuOpen = !menuOpen" aria-label="Buka menu">
      <span>{{ menuOpen ? '✕' : '☰' }}</span>
    </button>

    <nav class="nav-links" :class="{ 'nav-open': menuOpen }">
      <a href="#beranda" @click="closeMenu">Beranda</a>
      <a href="#katalog" @click="closeMenu">Katalog</a>
      <a href="#tentang" @click="closeMenu">Tentang Kami</a>
      <a href="#proses" @click="closeMenu">Cara Pesan</a>
      <a href="#kontak" class="nav-cta" @click="closeMenu">
        Hubungi Kami ↗
      </a>
    </nav>
  </header>
</template>
