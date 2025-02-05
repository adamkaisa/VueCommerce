<template>
  <div class="product-card">
    <img :src="`/images/${product.image}`" alt="product image" class="product-image" />
    <h3 class="product-name">{{ product.name }}</h3>
    <p class="product-price">${{ product.price }}</p>
    <p class="product-description">{{ product.description }}</p>
    <button @click="viewDetails(product)" class="view-details-btn">🔎 View Details</button>
  </div>
</template>

<script>
export default {
  props: {
    product: Object,
    isDarkMode: Boolean
  },
  methods: {
    viewDetails(product) {
      this.$emit('show-details', product);
    }
  }
}
</script>

<style scoped>
.product-card {
  background: var(--card-bg);
  border: 1px solid var(--border-color);
  border-radius: 10px;
  padding: 15px;
  text-align: center;
  transition: transform 0.3s ease;
  max-width: 250px;
  margin: 15px;
}

.product-card:hover {
  transform: translateY(-5px);
}

.product-image {
  width: 100%;
  height: auto;
  border-radius: 10px;
}

.product-name {
  font-size: 1.2rem;
  font-weight: bold;
}

.product-price {
  font-size: 1.1rem;
  color: green;
}

.product-description {
  color: #6a6a6a;
  font-size: 0.9rem;
}

.dark .product-description {
  color: #b4b4b4;
  font-size: 0.9rem;
}

.view-details-btn {
  background-color: #555;
  color: #fff;
  padding: 10px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.view-details-btn:hover {
  background-color: #333;
}
</style>
