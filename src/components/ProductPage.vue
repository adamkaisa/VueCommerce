<template>
    <div :class="{ dark: isDarkMode }">
      <main class="product-grid">
        <!-- Menampilkan daftar produk -->
        <ProductCard
          v-for="product in products"
          :key="product.id"
          :product="product"
          :is-dark-mode="isDarkMode"
          @show-details="showProductDetails"
        />
      </main>
    
      <!-- Container Card Detail Produk yang Tampil -->
      <div v-if="selectedProduct" class="product-detail-container">
        <div class="product-detail-card">
          <!-- Gambar Produk -->
          <div class="product-image-container">
            <img :src="`/images/${selectedProduct.images[selectedImageIndex]}`" alt="product image" class="product-image" />
            
            <!-- Navigasi Gambar (Panah Kiri/Kanan) di bawah gambar -->
            <div class="image-navigation">
              <button @click="previousImage" class="prev-btn">
                <i class="fa fa-arrow-left"></i>
              </button>
              <button @click="nextImage" class="next-btn">
                <i class="fa fa-arrow-right"></i>
              </button>
            </div>
          </div>
    
          <!-- Info Produk -->
          <div class="product-info-container">
            <h3 class="product-name">{{ selectedProduct.name }}</h3>
            <p class="product-price">${{ selectedProduct.price }}</p>
            <p class="product-description">{{ selectedProduct.description }}</p>
  
            <!-- Pilihan Warna -->
            <div class="color-options">
              <label>Choose a color:</label>
              <div class="color-palette">
                <div
                  v-for="color in selectedProduct.colors"
                  :key="color"
                  :class="['color-option', { selected: selectedColor === color }]"
                  :style="{ backgroundColor: color }"
                  @click="selectColor(color)"
                ></div>
              </div>
            </div>
  
            <!-- Pilihan Jumlah -->
            <div class="quantity-selector">
              <label for="quantity">Quantity:</label>
              <input type="number" id="quantity" v-model="quantity" min="1" max="10" />
            </div>
  
            <!-- Tombol Add to Cart -->
            <button @click="addToCart" class="add-to-cart-btn">🛒 Add to Cart</button>
          </div>
  
          <!-- Tombol Close (X) -->
          <button @click="closeDetails" class="close-detail-btn">×</button>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import ProductCard from '@/components/ProductCard.vue';
  import 'font-awesome/css/font-awesome.css';
  
  export default {
    components: {
      ProductCard
    },
    props: {
      isDarkMode: Boolean
    },
    data() {
      return {
        products: [
          { id: 1, name: 'Product 1', 
            price: 199.99, 
            description: 'This is a description for product 1', 
            image: 'image1.jpg', 
            colors: ['Red', 'Blue', 'Green'], 
            images: ['image1.jpg', 'image2.jpg', 'image3.jpg', 'image4.jpg', 'image5.jpg'] },
         
            { id: 2, 
              name: 'Product 2', 
              price: 149.99, 
              description: 'This is a description for product 2', 
              image: 'image2.jpg', colors: ['Black', 'White', 'Yellow'], 
              images: ['image2.jpg', 'image3.jpg', 'image4.jpg', 'image5.jpg', 'image2.jpg'] },

          { id: 3, 
            name: 'Product 3', 
            price: 199.99, 
            description: 'This is a description for product 3', 
            image: 'image3.jpg', colors: ['Gray', 'Pink', 'Purple'], 
            images: ['image3.jpg', 'image4.jpg', 'image5.jpg', 'image2.jpg', 'image3.jpg'] },

          { id: 4, 
            name: 'Product 4', 
            price: 199.99, 
            description: 'This is a description for product 4', 
            image: 'image4.jpg', colors: ['Brown', 'Orange', 'Silver'], 
            images: ['image4.jpg', 'image5.jpg', 'image1.jpg','image2.jpg', 'image3.jpg', 'image4.jpg'] }
        ],
        selectedProduct: null,
        selectedColor: '',
        quantity: 1,
        selectedImageIndex: 0
      };
    },
    methods: {
      showProductDetails(product) {
        this.selectedProduct = product;
        this.selectedColor = product.colors[0];
        this.selectedImageIndex = 0;
      },
      closeDetails() {
        this.selectedProduct = null;
      },
      addToCart() {
        if (this.selectedProduct) {
          console.log(`Added ${this.quantity} of ${this.selectedProduct.name} (Color: ${this.selectedColor}) to the cart.`);
        }
      },
      previousImage() {
        if (this.selectedImageIndex > 0) {
          this.selectedImageIndex--;
        }
      },
      nextImage() {
        if (this.selectedImageIndex < this.selectedProduct.images.length - 1) {
          this.selectedImageIndex++;
        }
      },
      selectColor(color) {
        this.selectedColor = color;
      }
    }
  };
  </script>
  
  <style scoped>
  .product-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 20px;
    padding: 20px;
  }
  
  .product-detail-container {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
    background-color: rgba(0, 0, 0, 0.5);
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 10;
  }
  
  .product-detail-card {
    background: var(--card-bg);
    display: flex;
    flex-direction: row;
    padding: 20px;
    border-radius: 10px;
    max-width: 800px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
    position: relative;
  }
  
  .product-image-container {
    flex: 1;
    padding-right: 20px;
    position: relative;
  }
  
  .product-image {
    width: 100%;
    height: auto;
    border-radius: 10px;
  }
  
   .image-navigation {
    position: absolute;
    bottom: 10px;
    left: 10px;
    right: 40px;
    display: flex;
    justify-content: space-between;
    padding: 0 20px;
    width: auto;
  }

   .prev-btn,
   .next-btn {
    background-color: rgba(0, 0, 0, 0.5);
    color: #fff;
    font-size: 18px;
    padding: 10px 15px;
    border: none;
    cursor: pointer;
    transition: background-color 0.3s;
    border-radius: 5px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

   .prev-btn:hover,
   .next-btn:hover {
    background-color: rgba(0, 0, 0, 0.8);
  }

    @media (max-width: 768px) {
    .image-navigation {
        bottom: 15px; 
        padding: 0 15px;
    }

    .prev-btn,
    .next-btn {
        font-size: 16px;
        padding: 8px 12px; 
    }
  }

    @media (max-width: 480px) {
    .image-navigation {
        bottom: 15px; 
        padding: 0 10px;
    }

    .prev-btn,
    .next-btn {
        font-size: 14px;
        padding: 6px 10px;
    }
  }

  .product-info-container {
    flex: 2;
    text-align: left;
  }
  
  .product-name {
    font-size: 1.5rem;
    font-weight: bold;
  }
  
  .product-price {
    font-size: 1.2rem;
    color: green;
  }
  
  .product-description {
    color: #777;
    font-size: 1rem;
    margin-bottom: 20px;
  }

  .dark .product-description {
    color: #adadad;
    font-size: 1rem;
    margin-bottom: 20px;
  }
  
  .color-options {
    margin-bottom: 20px;
  }
  
  .color-palette {
    display: flex;
    gap: 10px;
    margin-top: 10px;
  }
  
  .color-option {
    width: 30px;
    height: 30px;
    border-radius: 50%;
    cursor: pointer;
    transition: transform 0.2s, border 0.3s;
    border: 2px solid transparent;
  }
  
  .color-option.selected {
    border: 2px solid #fff;
  }
  
  .dark .color-option.selected {
    border: 2px solid #333;
  }
  
  body:not(.dark) .color-option {
    border: 2px solid #ccc;
  }
  
  body:not(.dark) .color-option.selected {
    border: 2px solid #000;
  }
  
  .quantity-selector {
    margin-bottom: 20px;
  }
  
  .quantity-selector input {
    padding: 5px;
    font-size: 1rem;
  }
  
  .add-to-cart-btn {
    background-color: #333;
    color: #fff;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .add-to-cart-btn:hover {
    background-color: #555;
  }
  
  .close-detail-btn {
    position: absolute;
    top: 10px;
    right: 10px;
    background-color: transparent;
    color: #fff;
    font-size: 2rem;
    border: none;
    cursor: pointer;
    transition: color 0.3s;
  }
  
  .dark .close-detail-btn {
    color: #fff;
  }
  
  .close-detail-btn {
    color: #333;
  }
  
  .close-detail-btn:hover {
    color: #bbb;
  }
  
  .dark {
    background-color: #333;
    color: #fff;
  }
  </style>
  