<template>
  <div class="m-2 w-96 shadow-2xl">
    <div class="m-2">
      <div class="font-bold">Reviews:</div>
      <hr />
      <div class="" v-for="(review, index) in reviews" :key="index">
        <div>{{ review.name }} gave this {{ review.rating }} stars.</div>
        <div>"{{ review.review }}"</div>
        <hr />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import type { PropType } from "vue"
import type { Review } from "types"
import { defineComponent } from "vue"
export default defineComponent({
  name: "Reviews",
  props: {
    reviews: {
      type: Array as PropType<Review[]>,
      required: true
    }
  }
})
</script>
