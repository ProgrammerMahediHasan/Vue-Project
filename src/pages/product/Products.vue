<template>
  <div class="container py-4">
    <h2 class="mb-4 text-center">Our Products</h2>

    <!-- Loading state -->
    <div v-if="loading" class="text-center py-5">
      <div class="spinner-border text-primary" role="status">
        <span class="visually-hidden">Loading...</span>
      </div>
    </div>

    <!-- Error state -->
    <div v-else-if="error" class="alert alert-danger text-center">
      {{ error }}
    </div>

    <!-- Products Grid -->
    <div v-else class="row g-3">
      <div
        class="col-lg-3 col-md-4 col-sm-6"
        v-for="product in products"
        :key="product.id"
      >
        <ProductCard :product="product" />
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import ProductCard from './ProductCard.vue';

interface Product {
  id: number;
  title: string;
  description: string;
  images: string[];
  price: number;
}

const products = ref<Product[]>([]);
const loading = ref(true);
const error = ref('');

async function fetchProducts() {
  loading.value = true;
  error.value = '';
  try {
    const res = await axios.get('https://api.escuelajs.co/api/v1/products');
    products.value = res.data;
  } catch (err: any) {
    error.value = 'Failed to fetch products. Please try again later.';
    console.error(err);
  } finally {
    loading.value = false;
  }
}

onMounted(() => {
  fetchProducts();
});
</script>

<style scoped>
.container {
  max-width: 1200px;
}

/* Optional: Add subtle hover animation to all cards */
.row .col-lg-3 .product-card .card {
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.row .col-lg-3 .product-card .card:hover {
  transform: translateY(-5px);
  box-shadow: 0 12px 25px rgba(0, 0, 0, 0.25);
}
</style>
