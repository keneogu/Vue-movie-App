<template>
<header class="flex justify-center align-center shadow-md p-5 bg-sky-500">
  <router-link to="/">
    <h1 class="text-xl font-bold text-sky-50"><span class="decoration-white pr-2">Movie</span>App</h1>
  </router-link>
</header>
<main>
  <router-view />
</main>
  
</template>

<style lang="scss">
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
  }
  body {
    background-color: rgb(3 105 161);
  }
</style>
