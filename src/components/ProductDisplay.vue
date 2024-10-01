<script setup>
import ProductDetails from './ProductDetails.vue'
import { ref, computed } from 'vue'
import ReviewList from './ReviewList.vue'
import ReviewForm from './ReviewForm.vue'

const props = defineProps({
  premium: {
    type: Boolean,
    required: true
  }
})

// const emit = defineEmits(['add-to-cart', 'remove-from-cart'])

const count = ref(0)

const product = ref('Socks')
const brand = ref('JVM Fashion')
const selectedVariant = ref(0)

const details = ref(['50% cotton', '30% wool', '20% polyester'])
const variants = ref([
  { id: 2234, color: 'green', image: './assets/images/socks_green.jpg', quantity: 50 },
  { id: 2235, color: 'blue', image: './assets/images/socks_blue.jpg', quantity: 0 }
])
const reviews = ref([])

const addToCart = () => {
  count.value++
}

const removeFromCart = () => {
  if (count.value > 0) {
    count.value--
  }
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
        <img :src="image" />
      </div>
      <div class="product-info">
        <div class="cart">
          <p>Cart({{ count }})</p>
        </div>
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

        <div class="button-group">
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
    </div>
    <div>
      <ReviewList v-if="reviews.length" :reviews="reviews"></ReviewList>
      <ReviewForm @review-submitted="addReview"></ReviewForm>
    </div>
  </div>
</template>
