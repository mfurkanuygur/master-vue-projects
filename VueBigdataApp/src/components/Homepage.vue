<template>
  <div class="homepage">
    <div v-if="products.length > 0">
      <div class="container">
        <RenderProduct
          v-for="product in products"
          :key="product.id"
          :product="product"
        />
      </div>
      <div class="see-more-container">
        <Loading v-if="loading" />
        <button v-else class="see-more-button" @click="handleClick">See more</button>
      </div>
    </div>
    <Loading v-else />
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { getAllProducts } from "../request/request";
import Loading from "./Loading.vue";
import RenderProduct from "./RenderProduct.vue";

const products = ref([]);
const skip = ref(0);
const loading = ref(false);

const fetchProducts = async () => {
  loading.value = true;
  const data = await getAllProducts(skip.value);
  products.value = [...products.value, ...data];
  loading.value = false;
};
onMounted(fetchProducts);

const handleClick = () => {
  skip.value += 10;
  fetchProducts();
};
</script>
