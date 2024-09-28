<script setup>
import { ref } from "vue"

import Button from "./Button.vue"
import ModalForm from "./ModalForm.vue"
import Book from "./Book.vue"

const date = new Date().toLocaleDateString("th-TH", {
  year: "2-digit",
  month: "short",
  day: "numeric",
})
const time = new Date().toLocaleTimeString("th-TH", {
  hour: "2-digit",
  minute: "2-digit",
})
const isEditing = ref(false)
const toggleEdit = () => {
  isEditing.value = !isEditing.value
}
const selectBooks = ref([])
const books = ref([
  {
    title: "Elment Online เล่ม 1",
    author: "Season Cloud",
    chapter: "ตอนที่ 1 : ไฟฉายย่อส่วน",
    imageUrl: "https://m1r.ai/OSERx.jpg",
  },
  {
    title: "Elment Online เล่ม 2",
    author: "Season Cloud",
    chapter: "ตอนที่ 2 : ไฟฉายย่อส่วน",
    imageUrl: "https://m1r.ai/XNF3.jpg",
  },
  {
    title: "Elment Online เล่ม 3",
    author: "Season Cloud",
    chapter: "ตอนที่ 3 : ไฟฉายย่อส่วน",
    imageUrl: "https://m1r.ai/AZl2K.jpg",
  },
  {
    title: "Elment Online เล่ม 4",
    author: "Season Cloud",
    chapter: "ตอนที่ 4 : ไฟฉายย่อส่วน",
    imageUrl: "https://m1r.ai/g5L7R.jpg",
  },
  {
    title: "Elment Online เล่ม 5",
    author: "Season Cloud",
    chapter: "ตอนที่ 5 : ไฟฉายย่อส่วน",
    imageUrl: "https://m1r.ai/8DoN.jpg",
  },
  {
    title: "Elment Online เล่ม 6",
    author: "Season Cloud",
    chapter: "ตอนที่ 6 : ไฟฉายย่อส่วน",
    imageUrl: "https://m1r.ai/pEal.jpg",
  },
])
const handleCreate = () => {
  createModal.showModal()
}
const deleteSelectedBooks = () => {
  selectBooks.value.forEach((selected, index) => {
    if (selected) {
      books.value.splice(index, 1)
      selectBooks.value.splice(index, 1)
    }
  })
}
</script>

<template>
  <div class="px-4 sm:px-8 lg:px-16 xl:px-60">
    <div class="ml-3 font-bold text-xl mt-10">รายการที่คั่นไว้</div>
    <div class="border-b border-gray-300 w-full mt-2"></div>
    <div class="mx-3">
      <div class="flex flex-col sm:flex-row justify-between items-center mt-5">
        <p class="mb-2 sm:mb-0">จำนวนทั้งหมด {{ books.length }} รายการ</p>
        <Button
          :isEditing="isEditing"
          :selectBooks="selectBooks"
          @handleCreate="handleCreate"
          @toggleEdit="toggleEdit"
          @deleteSelectedBooks="deleteSelectedBooks"
        />
      </div>

      <Book
        :books="books"
        :isEditing="isEditing"
        :selectBooks="selectBooks"
        :date="date"
        :time="time"
      />

      <ModalForm @handle-create="books.push($event)" />
    </div>
  </div>
</template>

<style scoped></style>
