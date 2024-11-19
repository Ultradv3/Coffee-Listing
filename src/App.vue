<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HomeView from './views/HomeView.vue'
import HeaderImg from './components/HeaderComponent/HeaderImg.vue'
</script>

<template>
  <HeaderImg />
  <RouterView />
</template>

<style scoped></style>
