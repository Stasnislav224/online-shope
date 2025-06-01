<script setup>
import {computed, ref, watch} from "vue";

const props = defineProps({
  id: Number,
  title: String,
  price: Number,
  image: String,
});

const count = ref(1);
const totalPrice = computed(() => count.value * props.price); 

const emit = defineEmits(['deleted-product']);

const deletedProduct = () => {
  emit('deleted-product', props.id);
}


watch(count, (newV) => {
  if (newV === 0) {
   deletedProduct() 
  }
})

</script>

<template>
  <li class="cart-item">
    <div class="product-img">
      <img
          :src="props.image"
          alt="product"
      >
    </div>
    <h3>{{props.title}}</h3>
    <div class="quantity">
      <input
          type="number"
          min="0"
          v-model="count"
      >
    </div>
    <div class="total-price">
      {{totalPrice}} $
    </div>
  </li>
</template>