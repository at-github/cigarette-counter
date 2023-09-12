<script setup lang="ts">
import { RouterView } from 'vue-router'
import AddCigaretteButton from './components/AddCigaretteButton.vue'
</script>

<template>
  <header>
    <h1>Compteur de cigarettes</h1>
  </header>

  <div class="container" style="margin-top: 80px">
    <AddCigaretteButton msg="Nouvelle clope" />
  </div>

  <RouterView />
</template>

<style scoped>
header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  padding: 20px;
  text-align: left;
}

h1 {
  color: #AAA;
  font-size: 1.5rem;
}
</style>
