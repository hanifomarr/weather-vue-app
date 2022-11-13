<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import InfoModal from './components/InfoModal.vue';
import NavBar from './components/NavBar.vue';
</script>

<template>
<div class="flex flex-col min-h-screen font-Roboto bg-color-primary">
  <NavBar />
  <InfoModal />
  <RouterView />
</div>
</template>

<style scoped>
</style>
