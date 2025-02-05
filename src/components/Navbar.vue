<template>
    <nav class="navbar">
      <div class="navbar-brand">
        <!-- Logo atau Nama Brand -->
        <router-link to="/" class="brand-name">VueCommerce</router-link>
      </div>
      <!-- Menu Navbar (desktop view) -->
      <div class="navbar-menu">
        <router-link to="/" class="navbar-btn">Home</router-link>
        <router-link to="/products" class="navbar-btn">Products</router-link>
        <button @click="toggleDarkMode" class="navbar-btn">
          {{ isDarkMode ? '☀️' : '🌙' }}
        </button>
      </div>
      <!-- Icon Menu (mobile view) -->
      <button class="menu-icon" @click="toggleMobileMenu">
        <i class="fa fa-bars"></i>
      </button>
    </nav>
  </template>
  
  <script>
  export default {
    props: {
      isDarkMode: Boolean,
    },
    data() {
      return {
        isMobileMenuOpen: false,
      };
    },
    methods: {
      toggleDarkMode() {
        this.$emit('toggle-dark-mode', !this.isDarkMode);
      },
      toggleMobileMenu() {
        this.isMobileMenuOpen = !this.isMobileMenuOpen;
      }
    }
  };
  </script>
  
  <style scoped>
  .navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: var(--bg-color);
    padding: 10px 20px;
    border-bottom: 2px solid var(--border-color);
    position: relative;
  }
  
  .navbar-brand .brand-name {
    font-size: 1.8rem;
    font-weight: bold;
    text-decoration: none;
    color: var(--button-text);
  }
  
  .navbar-menu {
    display: flex;
    gap: 20px;
  }
  
  .navbar-btn {
    background-color: var(--button-bg);
    color: var(--button-text);
    border: none;
    padding: 10px 20px;
    cursor: pointer;
    font-size: 1rem;
    border-radius: 5px;
    transition: all 0.3s ease;
    text-decoration: none;
  }
  
  .navbar-btn:hover {
    background-color: var(--link-hover-color);
    transform: scale(1.05);
  }
  
  .navbar-btn {
    display: inline-flex;
    align-items: center;
    gap: 8px;
  }
  
  .menu-icon {
    display: none;
    font-size: 2rem;
    background: none;
    border: none;
    color: var(--text-color);
    cursor: pointer;
  }
  
  @media (max-width: 768px) {
    .navbar-menu {
      display: none;
      flex-direction: column;
      position: absolute;
      top: 60px;
      right: 0;
      background-color: var(--bg-color);
      width: 100%;
      padding: 10px;
      border-top: 2px solid var(--border-color);
    }
  
    .navbar-menu.open {
      display: flex;
    }
  
    .menu-icon {
      display: block;
    }
  }
  </style>
  