<script setup>
import { defineProps } from "vue"

const props = defineProps({
  imageUrl: String,
})
</script>

<template>
  <header class="flex justify-center items-center overflow-hidden">
    <img
      v-if="imageUrl"
      :src="imageUrl"
      alt="Book Cover Banner"
      class="w-full h-[200px] object-cover"
    />
  </header>
</template>

<style scoped>
header {
  background-color: #f8f9fa;
  margin: 0; /* ลบ margin */
  padding: 0; /* ลบ padding */
  position: relative; /* เพื่อรองรับการจัดการ overflow */
}

html,
body {
  height: 100%; /* ตั้งค่าความสูงให้เต็ม */
}
</style>
