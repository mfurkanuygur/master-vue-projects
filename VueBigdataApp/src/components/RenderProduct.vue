<template>
  <div :key="product?.id" class="product-card">
    <div class="product-img">
      <img :src="product?.image" :alt="product?.title" />
    </div>
    <div class="product-body">
      <h3 class="product-title">{{ product?.title }}</h3>
      <div class="product-subtitle">
        <p class="product-price">${{ product?.price }}</p>
        <p class="product-cat">{{ product?.category }}</p>
      </div>
      <div class="buttons">
        <button class="product-button">
          <img :src="addcart" alt="addcart" />
        </button>
        <button class="product-button">
          <img :src="favorite" alt="favorite" />
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from "vue";
import addcart from "../assets/addcart.png";
import favorite from "../assets/favorite.png";

const props = defineProps({
  product: {
    type: Object,
    required: true,
  },
});
</script>
