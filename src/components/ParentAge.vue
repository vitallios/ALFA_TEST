<script setup>
import {ref} from 'vue'
const ParentAge = ref('')
</script>

<template>
  <div>
   <label for="parentAgeLabel"> Возраст </label>
   <input v-model="ParentAge" class="w-full border-none outline-none" type="text" id="parentAgeLabel">
  </div>
</template>