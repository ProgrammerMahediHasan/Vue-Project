<template>
  <div class="product-card">
    <div class="card">
      <img :src="product.images[0]" class="card-img" :alt="product.title" />
      <div class="card-body">
        <h5 class="card-title">{{ product.title }}</h5>
        <p class="card-text">{{ product.description }}</p>
        <a href="#" class="btn btn-primary">Add to Cart</a>
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  product: {
    type: Object,
    required: true
  }
});
</script>

<style scoped>
.product-card {
  display: flex;
  justify-content: center;
  margin: 1rem;
}

.card {
  width: 100%;
  max-width: 300px;
  border-radius: 12px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
  overflow: hidden;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  background-color: #fff;
}

.card:hover {
  transform: translateY(-5px);
  box-shadow: 0 12px 25px rgba(0, 0, 0, 0.25);
}

.card-img {
  width: 100%;
  height: 200px;
  object-fit: cover;
}

.card-body {
  padding: 1rem;
}

.card-title {
  font-size: 1.2rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
  color: #333;
}

.card-text {
  font-size: 0.95rem;
  color: #555;
  margin-bottom: 1rem;
}

.btn-primary {
  background-color: #007bff;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 6px;
  transition: background-color 0.3s ease;
}

.btn-primary:hover {
  background-color: #0056b3;
}
</style>
