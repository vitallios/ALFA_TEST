<script setup>
const props = defineProps(['btnText', 'iconBtn' ]);
</script>

<template>
 <button @click="$emit('addChild')" id="addChildBtn"
  class="btn absolute right-0 flex justify-between items-center px-[20px] py-[10px] border-[#01A7FD] border-[1px] rounded-[100px] outline-none">
  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
   <path fill-rule="evenodd" clip-rule="evenodd" fill="#01A7FD"  :d="iconBtn" />
  </svg>
  <span class="ml-[10px] text-[#01A7FD]">
   {{ btnText }}
  </span>
 </button>
</template>