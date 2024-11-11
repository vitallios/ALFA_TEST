<script setup>
import { RouterView } from 'vue-router'
import TheHeader from './components/TheHeader.vue'
import TheFooter from './components/TheFooter.vue'

</script>

<template>
  <TheHeader />
  <div class="container">
    <RouterView  />
  </div>
  <TheFooter />
</template>


<style>
@media  (max-width: 550px)  {
  .container{
    padding: 0 10px;
  }
}
</style>
