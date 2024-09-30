<script setup>
import ProductDetails from './ProductDetails.vue'
import { ref, computed } from 'vue'
import ReviewList from './ReviewList.vue'

const props = defineProps({
  premium: {
    type: Boolean,
    required: true
  }
})

const emit = defineEmits(['add-to-cart', 'remove-from-cart'])

const product = ref('Socks')
const brand = ref('Vue Mastery')
const selectedVariant = ref(0)
const details = ref(['50% cotton', '30% wool', '20% polyester'])
const variants = ref([
  { id: 2234, color: 'green', image: './assets/images/socks_green.jpg', quantity: 50 },
  { id: 2235, color: 'blue', image: './assets/images/socks_blue.jpg', quantity: 0 }
])
const reviews = ref([])

const addToCart = () => {
  emit('add-to-cart', variants.value[selectedVariant.value].id)
}

const removeFromCart = () => {
  emit('remove-from-cart', variants.value[selectedVariant.value].id)
}

const updateVariant = (index) => {
  selectedVariant.value = index
}

const addReview = (review) => {
  reviews.value.push(review)
}

const title = computed(() => {
  return brand.value + ' ' + product.value
})

const image = computed(() => {
  return variants.value[selectedVariant.value].image
})

const inStock = computed(() => {
  return variants.value[selectedVariant.value].quantity
})

const shipping = computed(() => {
  return props.premium ? 'Free' : 2.99
})
</script>

<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img width="100px" height="100px" :src="image" />
      </div>
      <div class="product-info">
        <h1>{{ title }}</h1>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        <p>Shipping: {{ shipping }}</p>
        <ProductDetails :details="details"></ProductDetails>
        <div
          v-for="(variant, index) in variants"
          :key="variant.id"
          @mouseover="updateVariant(index)"
          class="color-circle"
          :style="{ backgroundColor: variant.color }"
        ></div>

        <button
          class="button"
          :class="{ disabledButton: !inStock }"
          :disabled="!inStock"
          @click="addToCart"
        >
          Add to Cart
        </button>
        <button
          class="button"
          :class="{ disabledButton: !inStock }"
          :disabled="!inStock"
          @click="removeFromCart"
        >
          Remove from Cart
        </button>
      </div>
    </div>
    <div>
      <ReviewList v-if="reviews.length" :reviews="reviews"></ReviewList>
      <ReviewForm @review-submitted="addReview"></ReviewForm>
    </div>
  </div>
</template>
