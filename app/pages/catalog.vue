<script setup lang="ts">
import { product } from '~/data/mocks/products'
</script>

<template>
  <div class="grid">
    <ProductCard :product="product.product" />
  </div>
</template>

<style scoped>
.grid {
  width: 100%;
  display: grid;
  gap: 20px;
  grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
}
</style>