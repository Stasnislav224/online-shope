<script setup>
defineProps(['search', 'cart']);
const emit = defineEmits(['update:search', 'show-cart', 'show-sideBar']);
</script>

<template>
    <header>
        <div class="container header-container">
          <button 
            class="burger-menu"
            @click="$emit('show-sideBar')"
          >
            <div class="rectangle"></div>
            <div class="rectangle"></div>
            <div class="rectangle"></div>
            <div class="cross cross-1"></div>
            <div class="cross cross-1"></div>
          </button>
          <div class="logo">
              <a href="#">Logo</a>
          </div>
          <div class="header-items">
            <div 
            v-if="!cart"
            class="searchInput"
            >
              <input
                  type="text"
                  :value="search"
                  @input="$emit('update:search', $event.target.value)"
              >
            </div>
            <nav class="header-menu">
              <ul class="menu">
                <li>Home</li>
                <li
                    @click="$emit('show-cart')"
                >
                  Cart
                </li>
                <li>Category</li>
              </ul>
            </nav>
          </div>
        </div>
    </header>
</template>


