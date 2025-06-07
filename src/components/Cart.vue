<script setup>
import CartItem from "@/components/CartItem.vue";
import { computed } from "vue";


const props = defineProps({
    products: {
        type: Array,
    }
});

const deleteI = (id) => {
  const index = props.products.findIndex(item => item.id === id);
  props.products.splice(index, 1);

  localStorage.setItem('cart', JSON.stringify(props.products));
}

const filterItems = computed(() => {
    const arr = [];
    const seenIds = [];

    for (let i = 0; i < props.products.length; i++) {
        const currentItem = props.products[i];

        if (!seenIds[currentItem]) {
            arr.push(currentItem);
            seenIds[currentItem] = true;
        }

        const index = props.products.findIndex(item => currentItem.id === item.id);
        props.products.splice(index, 1);
    }

    return arr;
});


</script>

<template>
    <section>
    <h2 class="title cart-title">Cart</h2>
        <div class="container">
            <ul 
            v-if="props.products.length"
            class="cart-item-wrapper"
            >
            <CartItem
                v-for="product in filterItems"
                :key="product.title"
                :title="product.title"
                :image="product.image"
                :price="product.price"
                :id="product.id"
                @deleted-product="deleteI"
            />
            </ul>
            <template
            v-else
            >
            <h3 class="title">Not Found</h3>
            </template>
        </div>
    </section>
</template>


