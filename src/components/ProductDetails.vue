<template>
  <div v-for="detail in details">{{ detail }}</div>
</template>

<script lang="ts">
import type { PropType } from "vue"
import { defineComponent } from "vue"
export default defineComponent({
  name: "ProductDisplay",
  props: {
    details: {
      type: Array as PropType<string[]>,
      required: true
    }
  }
})
</script>
