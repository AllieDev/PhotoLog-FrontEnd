<template>
  <nav class="nav">
    <div class="nav__container">
      <p class="nav__logo">PhotoLog</p>
      <div class="nav__links">
        <RouterLink class="nav__link" to="/">Home</RouterLink>
        <RouterLink class="nav__link" to="/create">Create</RouterLink>
      </div>
    </div>
  </nav>
  <RouterView />
</template>

<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<style scoped>
.nav {
   font-family: sans-serif;
   background-color: rgb(0, 72, 255);
   height: 50px;
   display: flex;
   justify-content: center;
   align-items: center;
}
.nav__container {
  max-width: 1200px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 0 20px;
}
.nav__logo {
  color: white;
  
  font-size: x-large;
  font-weight: 600;
  font-style: italic;
}
.nav__links {
  width: 120px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.nav__link {
  color: white;
  text-decoration: none;
  font-size: medium;
}
</style>
