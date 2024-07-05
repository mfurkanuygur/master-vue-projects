<template>
  <div class="homepage">
    <!-- <h1>All Products: {{ products?.length }}</h1> -->
    <div v-if="products" class="container">
      <RenderProduct
        v-for="product in products.slice(0, count)"
        :key="product.id"
        :product="product"
      />
    </div>
    <Loading v-else />
    <div v-if="products" class="see-more-container">
      <button class="see-more-button" @click="handleClick">see more</button>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { getAllProducts } from '../request/request';
import Loading from './Loading.vue';
import RenderProduct from './RenderProduct.vue';

const products = ref(null);
const count = ref(10);

onMounted(async () => {
  const data = await getAllProducts();
  products.value = data;
});

const handleClick = () => {
  count.value += 10;
  console.log(count.value);
};
</script>
