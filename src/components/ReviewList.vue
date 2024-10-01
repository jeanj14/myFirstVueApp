<script setup>
import { defineProps } from 'vue'
import StarRating from 'vue-star-rating'

const props = defineProps({
  reviews: {
    type: Array,
    required: true
  }
})
//  to-do later

// const showStars = computed(() => {
//   return (rating) => {
//     let stars = ''
//     for (let index = 0; index < rating; index++) {
//       stars += '⭐' // Unicode star character
//     }
//     return stars
//   }
// })
</script>

<template>
  <div class="review-container">
    <h3>Reviews:</h3>
    <ul>
      <li v-for="(review, index) in props.reviews" :key="index">
        {{ review.name }}
        <br />
        "{{ review.review }}"
        <br />
        <star-rating
          v-model:rating="review.rating"
          :show-rating="false"
          :read-only="true"
        ></star-rating>
        <br />
        <span id="recommend" v-if="review.recommendation">They recommend this product!</span>
        <br />
      </li>
    </ul>
  </div>
</template>
