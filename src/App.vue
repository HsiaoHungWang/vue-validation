<script setup>
import { RouterLink, RouterView } from 'vue-router'
import Navbar from './components/Navbar.vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import 'bootstrap/dist/js/bootstrap.js'
import 'bootstrap-icons/font/bootstrap-icons.css'


</script>

<template>
  <div class="container">
    <Navbar></Navbar>

    <RouterView />
  </div>
</template>

<style scoped></style>
