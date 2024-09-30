<script setup>
// import { RouterLink, RouterView } from 'vue-router'
import ProductDetails from './components/ProductDetails.vue'
import ProductDisplay from './components/ProductDisplay.vue'
// import ref from 'vue'

// const prod = ref(['shoes', 'Shop'])
</script>

<template>
  <header>
    <div class="">
      <!-- product details components
        -->
      <!-- <ProductDetails :details="['shoes', 'Shop']" /> -->
      <ProductDisplay />

      <!-- <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav> -->
    </div>
  </header>

  <!-- <RouterView /> -->
</template>

<style scoped></style>
