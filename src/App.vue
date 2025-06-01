<script setup>
import Header from "@/components/Header.vue";
import ProductItem from "@/components/ProductItem.vue";
import Cart from "@/components/Cart.vue";
import axios  from "axios";
import {ref, onMounted, computed, reactive} from "vue";


const products = ref([]);
const search = ref('');
const cart = reactive([]);
const showCart = ref(false);


const getProduct = async () => {
    try {
        const response = await axios.get(`https://fakestoreapi.com/products`);
        products.value = response.data;
    }
    catch(error) {
        console.error(error);
    }
}

const cartItem = (id) => {
  cart.forEach(product => console.log(product));

  cart.push(products.value.filter(product => product.id === id));
}

onMounted(() => {
    getProduct();
});

const filterProducts = computed(() => {
  if (!search.value) return products.value;

  return products.value.filter(product =>
      product.title.toLowerCase().indexOf(search.value.toLowerCase()) !== -1
  );
});


const showCartsItem = () => {
  showCart.value = !showCart.value;
}
</script>

<template>
  <Header
      v-model:search="search"
      @show-cart="showCartsItem"
      :cart="showCart"
  />
  <main>
    <Cart
        v-if="showCart"
        :products="cart || []"
    />
    <section
        class="shop-wrapper"
        v-if="!showCart"
    >
      <ProductItem
          v-for="product in filterProducts"
          :key="product.id"
          :title="product.title"
          :price="product.price"
          :image="product.image"
          @buy="cartItem(product.id)"
      />
    </section>
  </main>
</template>