<script setup lang="ts">
import { RouterView } from 'vue-router'
import CityList from './components/CityList.vue';
import NavBar from './components/NavBar.vue';
</script>

<template>
<div class="flex flex-col min-h-screen font-Roboto bg-color-primary">
  <NavBar />
  <RouterView />
</div>
</template>

<style scoped>
</style>
