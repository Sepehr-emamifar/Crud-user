<script setup>
import Navbar from "@/components/Navbar.vue";
</script>

<template>
  <div>
    <Navbar />
  </div>
  <div class="max-w-7xl mx-auto mt-10 py-4 px-8">
    <RouterView />
  </div>
</template>

<style scoped></style>
