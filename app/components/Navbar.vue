
<script setup>
import { ref } from 'vue'

const isMenuOpen = ref(false)

function toggleMenu() {
  isMenuOpen.value = !isMenuOpen.value
}
</script>

<template>
  <header :class="{ open: isMenuOpen }">

    <!-- LOGO -->
    <div class="logo">MYKOO</div>

    <!-- MOBILE HAMBURGER -->
    <div
      id="hamburger"
      class="hamburger"
      @click="toggleMenu"
    >
      {{ isMenuOpen ? '✖' : '☰' }}
    </div>

    <!-- NAVIGATION -->
    <div class="breadcrumbs">
      <ul>
        <li>
          <NuxtLink to="/" @click="isMenuOpen = false">
            Home
          </NuxtLink>
        </li>

        <li>
          <NuxtLink to="/about-me" @click="isMenuOpen = false">
            About
          </NuxtLink>
        </li>

        <li>
          <NuxtLink to="/tech-stack" @click="isMenuOpen = false">
            Tech Stack
          </NuxtLink>
        </li>

        <li>
          <NuxtLink to="/cert" @click="isMenuOpen = false">
            Certification
          </NuxtLink>
        </li>
      </ul>
    </div>

  </header>
</template>
