<script setup>
import { ref, computed } from "vue"
import banner_1 from "../assets/banner/banner_1.png"
import banner_2 from "../assets/banner/banner_2.png"
import banner_3 from "../assets/banner/banner_3.png"
import banner_4 from "../assets/banner/banner_4.png"
import banner_5 from "../assets/banner/banner_5.png"

const currentBanner = ref(0)
const banners = [banner_1, banner_2, banner_3, banner_4, banner_5]

const handleNext = () => {
  currentBanner.value = (currentBanner.value + 1) % banners.length
}

const handlePrev = () => {
  currentBanner.value =
    (currentBanner.value - 1 + banners.length) % banners.length
}

const prevBanner = computed(() => {
  return (currentBanner.value - 1 + banners.length) % banners.length
})

const nextBanner = computed(() => {
  return (currentBanner.value + 1) % banners.length
})

console.log(banners)
console.log(currentBanner.value)
</script>

<template>
  <div class="relative w-full">
    <div class="flex flex- justify-center items-center">
      <img
        :src="banners[prevBanner]"
        alt="Previous Banner"
        class="w-0 h-64 lg:h-96 lg:w-1/2 xl:h-96 xl:w-1/2"
      />
      <img
        :src="banners[currentBanner]"
        alt="Current Banner"
        class="w-full h-64 lg:h-96 lg:w-1/2 xl:h-96"
      />
      <img
        :src="banners[nextBanner]"
        alt="Next Banner"
        class="w-0 h-64 xl:h-96 xl:w-1/2"
      />
    </div>
    <div
      class="absolute left-5 right-5 top-1/2 flex -translate-y-1/2 transform justify-between"
    >
      <button class="btn btn-circle" @click="handlePrev">❮</button>
      <button class="btn btn-circle" @click="handleNext">❯</button>
    </div>
  </div>
</template>

<style>

</style>
