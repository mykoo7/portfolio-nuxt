<template>
  <header :class="{ open: isMenuOpen }">

    <!--LOGO-->
    <NuxtLink to="/" class="logo hover:text-rose-500 hover:scale-105 transition-all duration-300 cursor-pointer hover:shadow-rose-950/40">
      MYKOO
    </NuxtLink>

    <!--MOBILE HAMBURGER-->
    <div id="hamburger"
      class="hamburger"
      @click="toggleMenu"
    >
      {{ isMenuOpen ? '✖' : '☰' }}
    </div>

    <!--NAVIGATION-->
    <div class="breadcrumbs">
      <ul>
        <li>
          <NuxtLink to="/" @click="isMenuOpen = false" class="inline-flex items-center gap-2">
            <PhHouse :size="20" weight="regular" />
            Home
          </NuxtLink>
        </li>

        <li>
          <NuxtLink to="/about-me" @click="isMenuOpen = false" class="inline-flex items-center gap-2">
            <PhUser :size="20" weight="regular" />
            About
          </NuxtLink>
        </li>

        <li>
          <NuxtLink to="/tech-stack" @click="isMenuOpen = false" class="inline-flex items-center gap-2">
            <PhCode :size="20" weight="regular" />
            Tech Stack
          </NuxtLink>
        </li>

        <li>
          <NuxtLink to="/cert" @click="isMenuOpen = false" class="inline-flex items-center gap-2">
            <PhCertificate :size="20" weight="regular" />
            Certification
          </NuxtLink>
        </li>
      </ul>
    </div>

  </header>
</template>

<script setup>
import {PhHouse, PhUser, PhCode, PhCertificate} from '@phosphor-icons/vue' // USE PHOSPHOR ICON
import { ref } from 'vue'

const isMenuOpen = ref(false)

function toggleMenu() {
  isMenuOpen.value = !isMenuOpen.value
}
</script>
