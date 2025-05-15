<template>
  <NavBar/>
  <main class="pt-20">
    <slot />
  </main>
  <Footer />
</template>

<script setup>
import Header from '~/components/Header.vue'
import Footer from '~/components/Footer.vue'
import NavBar from '~/components/NavBar.vue'
</script>
