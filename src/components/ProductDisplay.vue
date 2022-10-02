<template>
  <div class="flex">
    <img class="w-96 shadow-2xl m-2" :class="inventory === 0 && 'opacity-50'" :src="image" />
    <div class="flex flex-col justify-between m-2">
      <div>
        <div class="text-3xl font-bold">{{ title }}</div>
        <div>{{ description }}</div>
        <div>
          {{
            inventory > 10
              ? "In stock"
              : inventory <= 10 && inventory > 0
              ? "Almost sold out"
              : "Out of stock"
          }}
        </div>
        <div v-show="isOnSale">{{ onSaleMessage }}</div>
        <div class="mt-5 font-bold">Material:</div>
        <ProductDetails :details="details" />
      </div>
      <div>
        <div class="mt-5 font-bold">Colors:</div>
        <div class="flex">
          <div
            :class="
              'w-10 h-10 rounded-full border-[1px] border-black cursor-pointer mr-1 bg-' +
              variant.color +
              '-500'
            "
            v-for="(variant, index) in variants"
            :key="variant.id"
            @mouseover="() => updateVariant(index)"></div>
        </div>
        <div class="mt-5 font-bold">Sizes:</div>
        <div class="flex">
          <div class="mx-1" v-for="(size, index) in sizes" :key="index">{{ size }}</div>
        </div>
      </div>
    </div>
    <div class="flex flex-col justify-end m-2">
      <div class="text-center py-1">Shipping: {{ shippingFee }}</div>
      <button
        class="shadow-2xl py-1 px-5"
        :class="inventory === 0 ? 'bg-gray-500' : 'bg-green-500 hover:bg-green-600'"
        :disabled="inventory === 0"
        @click="incrementCart(selectedVariant)">
        Add to Cart
      </button>
      <button
        class="shadow-2xl py-1 px-5 mt-2"
        :class="
          cart.length === 0 || variants[selectedVariant].quantity === 0
            ? 'bg-gray-500'
            : 'bg-red-500 hover:bg-red-600'
        "
        :disabled="cart.length === 0 || variants[selectedVariant].quantity === 0"
        @click="decrementCart(selectedVariant)">
        Remove from Cart
      </button>
    </div>
  </div>
</template>

<script lang="ts">
import type { PropType } from "vue"
import { defineComponent } from "vue"
import ProductDetails from "./ProductDetails.vue"
export default defineComponent({
  name: "ProductDisplay",
  components: { ProductDetails },
  props: {
    premium: {
      type: Boolean,
      required: true
    },
    cart: {
      type: Array as PropType<number[]>,
      required: true
    }
  },
  data() {
    return {
      product: "Socks",
      brand: "Nico's",
      selectedVariant: 0,
      description: "A warm fuzzy pair of socks.",
      isOnSale: false,
      details: ["50% cotton", "30% wool", "20% polyester"],
      variants: [
        { id: 1, color: "green", image: "../src/assets/socks_green.jpg", quantity: 11 },
        { id: 2, color: "blue", image: "../src/assets/socks_blue.jpg", quantity: 1 }
      ],
      sizes: ["S", "M", "L"]
    }
  },
  methods: {
    incrementCart(index: number) {
      const amount = this.cart.filter((item) => item === this.selectedVariant).length
      if (amount >= this.variants[this.selectedVariant].quantity) return
      this.$emit("incrementCart", index)
    },
    decrementCart(index: number) {
      const amount = this.cart.filter((item) => item === this.selectedVariant).length
      if (amount > this.variants[this.selectedVariant].quantity) return
      this.$emit("decrementCart")
    },
    updateVariant(index: number) {
      this.selectedVariant = index
    }
  },
  computed: {
    title() {
      return `${this.brand} ${this.product}`
    },
    image() {
      return this.variants[this.selectedVariant].image
    },
    inventory() {
      return this.variants[this.selectedVariant].quantity
    },
    onSaleMessage() {
      return `${this.brand} ${this.product} are on sale`
    },
    shippingFee() {
      if (this.premium) return "Free"
      return "$2.99"
    }
  }
})
</script>
