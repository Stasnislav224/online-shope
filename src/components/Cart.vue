<script setup>
import CartItem from "@/components/CartItem.vue";


const props = defineProps(['products']);

const deleteI = (id) => {
  const index = props.products.findIndex(item => item.id === id);
  props.products.splice(index, 1);
}

</script>

<template>
    <section>
    <h2 class="title cart-title">Cart</h2>
        <div class="container">
            <ul 
            v-if="props.products.length"
            class="cart-item-wrapper"
            >
              <template
                  v-for="products in props.products"
              >
                <CartItem
                    v-for="product in products"
                    :key="product.title"
                    :title="product.title"
                    :image="product.image"
                    :price="product.price"
                    :id="product.id"
                    @deleted-product="deleteI"
                />
              </template>
            </ul>
            <template
            v-else
            >
            <h3 class="title">Not Found</h3>
            </template>
        </div>
    </section>
</template>


