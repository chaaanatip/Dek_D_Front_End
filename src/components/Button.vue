<script setup>
import { defineProps, defineEmits } from "vue"
import IconBin from "./icons/IconBin.vue"

const props = defineProps({
  isEditing: Boolean,
  selectBooks: Array,
})

const emit = defineEmits(["handleCreate", "toggleEdit", "deleteSelectedBooks"])
</script>

<template>
  <div class="flex space-x-3">
    <button @click="$emit('handleCreate')" class="btn bg-green-300 rounded-xl text-white">
      สร้างหนังสือ
    </button>
    <button
      @click="$emit('toggleEdit')"
      :class="
        isEditing
          ? 'border-gray-500 text-gray-500'
          : 'bg-orange-200 text-orange-500'
      "
      class="btn rounded-xl px-5"
    >
      <span>{{ isEditing ? "ยกเลิก" : "แก้ไข" }}</span>
    </button>
    <button
      v-if="isEditing && selectBooks.includes(true)"
      @click="$emit('deleteSelectedBooks')"
      class="btn  bg-red-400 rounded-3xl"
    >
      <IconBin class="w-5" />
    </button>
  </div>
</template>

<style scoped></style>
