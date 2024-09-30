<script setup>
import { ref } from 'vue'

const emit = defineEmits(['review-submitted'])

const name = ref('')
const reviewText = ref('')
const rating = ref(null)
const recommendation = ref(false)

const onSubmit = () => {
  if (name.value === '' || reviewText.value === '' || rating.value === null) {
    alert('Please fill out the information before submitting the form')
    return
  }

  const productReview = {
    name: name.value,
    review: reviewText.value,
    rating: rating.value,
    recommendation: recommendation.value
  }

  emit('review-submitted', productReview)

  // Reset form fields
  name.value = ''
  reviewText.value = ''
  rating.value = null
  recommendation.value = false
}
</script>

<template>
  <form class="review-form" @submit.prevent="onSubmit">
    <h3>Leave a review</h3>
    <label for="name">Name:</label>
    <input id="name" v-model="name" />
    <label for="review">Review:</label>
    <textarea id="review" v-model="reviewText"></textarea>
    <label for="rating">Rating:</label>
    <select id="rating" v-model.number="rating">
      <option>5</option>
      <option>4</option>
      <option>3</option>
      <option>2</option>
      <option>1</option>
    </select>

    <label for="recommendation">Would you recommend this product?</label>
    <input type="checkbox" v-model="recommendation" id="recommendation" />
    <input class="button" type="submit" value="Submit" />
  </form>
</template>
