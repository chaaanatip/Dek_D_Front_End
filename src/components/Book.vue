<script setup>
import { defineProps } from "vue"
import IconList from "./icons/IconList.vue"
import IconBookmark from "./icons/IconBookmark.vue"
const props = defineProps({
  books: {
    type: Array,
    required: true,
  },
  isEditing: Boolean,
  selectBooks: Array,
  date: String,
  time: String,
})
</script>
<template>
  <div
    class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-2 xl:grid-cols-3 gap-4"
  >
    <div v-for="(book, index) in books" :key="index" class="flex mt-5 p-2">
      <img
        :src="book.imageUrl"
        alt=""
        class="w-2/4 h-5/4 md:w-5/4 md:h-5/4 rounded-[10px]"
      />
      <div class="ml-3 pr-10">
        <p class="font-bold text-xl">{{ book.title }}</p>
        <p class="mt-1">{{ book.author }}</p>
        <div class="flex items-center mt-10 text-gray-400">
          <IconList />
          <p class="ml-2 flex mb-1">{{ book.chapter }}</p>
        </div>
        <div class="flex items-center text-gray-400">
          <IconBookmark />
          <p class="ml-2 flex mb-1">คั่นล่าสุด {{ date }} / {{ time }} น.</p>
        </div>
      </div>
      <input
        v-if="isEditing"
        type="checkbox"
        v-model="selectBooks[index]"
        class="ml-2"
      />
    </div>
  </div>
</template>

<style scoped></style>
