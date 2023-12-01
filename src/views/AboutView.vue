<script setup>
  import API from '../components/Api.vue'
</script>
<template>
  <div class="about justify-center px-10 lg:p-0">
    <API></API>
  </div>
</template>

<style>

@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
