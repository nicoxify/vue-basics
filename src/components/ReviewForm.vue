<template>
  <div class="shadow-2xl w-96 m-2">
    <form @submit.prevent="onSubmit">
      <div class="m-2 font-bold">Leave a review</div>
      <div class="flex flex-col m-2">
        <label for="name">Your name:</label>
        <input class="shadow-xl" id="name" v-model="name" />
        <label class="mt-2" for="review">Reviewtext:</label>
        <textarea class="shadow-xl" id="review" v-model="review" />
        <label class="mt-2" for="rating">Rating:</label>
        <select class="shadow-xl py-2" id="rating" v-model="rating">
          <option>1</option>
          <option>2</option>
          <option>3</option>
          <option>4</option>
          <option>5</option>
        </select>
        <button class="mt-2 shadow-xl py-1 bg-green-500 hover:bg-green-600" type="submit">
          Submit
        </button>
      </div>
    </form>
  </div>
</template>

<script lang="ts">
import type { Review } from "../../types"
import { defineComponent } from "vue"
export default defineComponent({
  name: "ReviewForm",
  data() {
    return {
      name: "",
      review: "",
      rating: 5,
      reviews: [] as Review[]
    }
  },
  methods: {
    onSubmit() {
      if (this.name === "" || this.review === "") return alert("Please fill out every field")
      const productReview = {
        name: this.name,
        review: this.review,
        rating: +this.rating
      }
      this.$emit("submit-review", productReview)
      this.name = ""
      this.review = ""
      this.rating = 5
    }
  }
})
</script>
