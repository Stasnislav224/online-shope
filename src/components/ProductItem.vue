<script setup>
defineProps(['title', 'price', 'image']);
defineEmits(['buy']);
</script>

<template>
  <div class="cart">
    <div class="cart-img">
      <img
          class="product-img"
          :src="image"
          alt="product"
      >
    </div>
    <h3 class="title">{{title}}</h3>
    <p class="price">
      {{price}} $
    </p>
    <button
        type="button"
        @click="$emit('buy')"
    >
      Add to cart
    </button>
  </div>
</template>