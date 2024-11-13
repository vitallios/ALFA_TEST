<script setup>
import {ref} from 'vue'
const ParentName = ref('')
</script>

<template>
  <div>
   <label for="parentNameLabel"> Имя </label>
   <input v-model="ParentName" class="w-full border-none outline-none" type="text" id="parentNameLabel">
  </div>
</template>
