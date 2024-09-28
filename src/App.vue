<script setup>
import { RouterLink, RouterView } from "vue-router"
import Banner from "./components/Banner.vue"
import Main from "./components/Main.vue"
</script>

<template>
  <div>
    <Banner />

    <RouterView />
  </div>
</template>

<style scoped></style>
