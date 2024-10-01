<script setup>
// import { RouterLink, RouterView } from 'vue-router'
import ProductDetails from './components/ProductDetails.vue'
import ProductDisplay from './components/ProductDisplay.vue'
// import ref from 'vue'

// const prod = ref(['shoes', 'Shop'])
</script>

<template>
  <div class="nav-bar"></div>
  <header>
    <div class="">
      <!-- product details components
        -->
      <!-- <ProductDetails :details="['shoes', 'Shop']" /> -->
      <ProductDisplay :premium="premium" @add-to-cart="updateCart" @remove-from-cart="removeById" />
      <ProductDetails />

      <!-- <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav> -->
    </div>
  </header>

  <!-- <RouterView /> -->
</template>

<style scoped></style>
