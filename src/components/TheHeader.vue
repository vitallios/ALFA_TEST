<template>
 <header class="HeaderShadow">
  <nav class="flex  w-full  items-center p-4 relative justify-center">
   <router-link to="/" class="absolute left-10">
   <img src="../assets/Logo.png" alt="">
   </router-link>
   <ul class="menu flex gap-[24px]  ">
    <li><router-link to="/">Форма</router-link></li>
    <li><router-link to="/about">Превью</router-link></li>
   </ul>
  </nav>
 </header>
</template>

<style scoped>
ul>li>a {
 color: var(--lightBlack);
}
</style>>

