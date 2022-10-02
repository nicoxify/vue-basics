<template>
  <div class="min-h-[95vh]">
    <div class="bg-green-500 flex justify-between items-center">
      <div class="m-2 text-2xl font-bold">Vue Project</div>
      <div class="shadow py-1 px-5 m-2">Cart({{ cart.length }})</div>
    </div>
    <ProductDisplay
      :premium="premium"
      :cart="cart"
      @incrementCart="incrementCart"
      @decrementCart="decrementCart" />
    <div class="flex items-start">
      <ReviewForm @submit-review="submitReview" />
      <Reviews v-if="reviews.length" :reviews="reviews" />
    </div>
  </div>
  <div class="h-[5vh] flex justify-center">
    <a class="p-1" target="_blank" :href="url">Made by Nico</a>
  </div>
</template>

<script lang="ts">
import type { Review } from "../types"
import { defineComponent } from "vue"
import ProductDisplay from "./components/ProductDisplay.vue"
import Reviews from "./components/Reviews.vue"
import ReviewForm from "./components/ReviewForm.vue"
export default defineComponent({
  name: "App",
  components: {
    ProductDisplay,
    Reviews,
    ReviewForm
  },
  data() {
    return {
      cart: [] as number[],
      reviews: [] as Review[],
      url: "https://portfolio-lyart-eight-32.vercel.app/",
      premium: true
    }
  },
  methods: {
    incrementCart(id: number) {
      this.cart.push(id)
    },
    decrementCart() {
      this.cart.pop()
    },
    submitReview(review: Review) {
      this.reviews.push(review)
    }
  }
})
</script>
