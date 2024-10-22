<!-- src/App.js -->
<script setup>
import { RouterView } from 'vue-router';
import Navbar from './components/Navbar.vue';
import CountriesList from './components/CountriesList.vue';



</script>


<template>
  <div class="app">
    <Header></Header>
    <Navbar></Navbar>
    <RouterView></RouterView>
  </div>
  
</template>