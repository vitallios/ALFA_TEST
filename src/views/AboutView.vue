<script setup>
import { ref, reactive } from 'vue';

defineProps({
  
})


const Parent = reactive({
  name: '',
  age: '',
  childtern: [],
});
</script>

<template>
  <div class="Preview">
    <div>
      <h3>Персональные данные</h3>
      <h2>Имя: {{Parent.name}}</h2><h2>Возраст: {{Parent.age}}</h2>
    </div>
    
    <div>
      <h3>Дети</h3>
      <ul>
        <li v-for="child in Parent.childtern" :key="child.age">
          <h2>Имя: {{child.name}}</h2><h2>Возраст: {{child.age}}</h2>
        </li>
      </ul>
    </div>
  </div>
</template>

