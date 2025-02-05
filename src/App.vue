<template>
  <div>
    <!-- Navbar -->
    <Navbar :is-dark-mode="isDarkMode" @toggle-dark-mode="toggleDarkMode" />
    <!-- Main Content -->
    <router-view />
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue';
import './assets/base.css'; 
import './assets/main.css';

export default {
  components: {
    Navbar,
  },
  data() {
    return {
      isDarkMode: false,
    };
  },
  methods: {
    toggleDarkMode(isDark) {
      this.isDarkMode = isDark;
      if (isDark) {
        document.documentElement.classList.add('dark');
      } else {
        document.documentElement.classList.remove('dark');
      }
    }
  }
};
</script>
