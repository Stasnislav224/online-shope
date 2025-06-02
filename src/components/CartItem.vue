<script setup>
import {computed, ref, watch} from "vue";

const props = defineProps({
  id: Number,
  title: String,
  price: Number,
  image: String,
});

const count = ref(1);
const totalPrice = computed(() => Math.round(count.value * props.price)); 

const emit = defineEmits(['deleted-product']);

const deletedProduct = () => {
  emit('deleted-product', props.id);
}

const action = () => {
  return {
    incr: function () { 
      count.value++;
    },
    decr: function () {
      count.value--;
    }
  }
}

const operation = action();

watch(count, (newV) => {
  if (newV === 0) {
   deletedProduct() 
  }
})

</script>

<template>
  <li 
  class="cart-item"
  v-if="count != 0"
  >
    <div class="product-img">
      <img
          :src="props.image"
          alt="product"
      >
    </div>
    <h3>{{props.title}}</h3>
    <div class="quantity">
    <button 
    class="count-btn"
    type="button"
    @click="operation.incr"
    >
    +
    </button>
      <input
          type="number"
          min="0"
          step="1"
          v-model="count"
      >
    <button 
    class="count-btn"
    type="button"
    @click="operation.decr"
    >
    -
    </button>
    </div>
    <div class="total-price">
      {{totalPrice}} $
    </div>
  </li>
</template>