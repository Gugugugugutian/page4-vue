<script setup>
import { RouterLink, RouterView } from 'vue-router'
import Top from '@/components/Top.vue'  
</script>

<script>
export default {
  name: 'App',
  components: {
    RouterLink,
    RouterView,
    Top
  },
  data() {
    return {
      dark: false
    }
  },
  props: {
  },
  methods: {
    switchDark() {
      this.dark = !this.dark;
    }
  },
  mounted() {
    this.dark = window.matchMedia('(prefers-color-scheme: dark)').matches;
  }
}
</script>

<template>
  <Top :class="{ 'dark-only-font': dark }" class="main-top" @change-dark="switchDark"></Top>
  <div class="main" :class="{ dark: dark }">
  </div>

</template>

<style scoped>
.main {
  min-height: 100vh;
  max-height: 100vh;
  transition: all 1s ease-in-out;
}
.main-top {
  transition: all 1s ease-in-out;
}
.dark-only-font {
  color: #fff;
}
.dark {
  background-color: #333;
  color: #fff;
}
</style>
