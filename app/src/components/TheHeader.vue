<template>
  <div>
    <header class="text-center m-auto">
      <h1 class="text-3xl my-8 m-auto text-[#deb363]">Crimes in New York City</h1>
      <p class="text-xs text-[#3d3637]">(well well well...)</p>
    </header>
    <nav class="container m-auto flex justify-center my-5">
      <router-link
        to="/"
        class="text-[#fff8a5] m-auto dark:md:hover:bg-yellow-600 transition duration-300"
        >Home</router-link
      >
      <router-link
        to="skincolor"
        class="text-[#fff8a5] m-auto dark:md:hover:bg-yellow-600 transition duration-300"
        >Color Chart</router-link
      >
      <router-link
        to="crime"
        class="text-[#fff8a5] m-auto dark:md:hover:bg-yellow-600 transition duration-300"
        >Crime Chart</router-link
      >
      <router-link
        to="borough"
        class="text-[#fff8a5] m-auto dark:md:hover:bg-yellow-600 transition duration-300"
        >Borough Chart</router-link
      >
    </nav>
  </div>
</template>

<script setup></script>

<style scoped></style>
