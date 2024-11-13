<script setup>
const props = defineProps(['saveTextBtn']);

</script>

<template>
 <button @click="$emit('save')"
  class="mt-[30px] py-[10px] px-[20px] border-[#01A7FD] border-[1px] rounded-[100px] bg-[#01A7FD] text-white text-[14px]">
  {{saveTextBtn}}
 </button>
</template>