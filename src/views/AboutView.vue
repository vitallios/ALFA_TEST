<script setup>
import { reactive } from 'vue';

const Parent = reactive({
  name: '',
  age: '',
  childtern: []
});

let ParentStore = JSON.parse(localStorage.getItem('Parent'));

Parent.name = ParentStore.name;
Parent.age = ParentStore.age;
Parent.childtern = ParentStore.childtern;

</script>

<template>
  <div class="Preview">
    <div class="flex flex-col gap-[20px] mt-[30px]">
      <h3>Родитель</h3>
      <h2 class="infoParent font-bold">{{ Parent.name }}, {{ Parent.age }}</h2>
    </div>
    <div class="mt-[60px] flex flex-col gap-[20px]">
      <h3>Дети</h3>
      <ul class="flex flex-col gap-[20px]">
        <li v-for="child in Parent.childtern" :key="child.age">
          <h2 class="px-[20px] py-[10px] bg-[#F2F2F2] rounded max-w-fit font-bold">
            {{ child.name }}, {{ child.age }}
          </h2>
        </li>
      </ul>
    </div>
  </div>
</template>
