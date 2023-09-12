<script setup lang="ts">
import { RouterView } from 'vue-router'
import AddCigaretteButton from './components/AddCigaretteButton.vue'
</script>

<template>
  <header>
    <div class="wrapper">
      <AddCigaretteButton msg="WIP - Nouvelle clope" />
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
</style>
