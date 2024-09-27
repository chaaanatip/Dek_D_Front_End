<script setup>
import { ref } from "vue"
import iconBin from "../components/icons/IconBin.vue"
const isEditing = ref(false)
const toggleEdit = () => {
  isEditing.value = !isEditing.value
}
const isCreating = ref(false)
const toggleCreate = () => {
  isCreating.value = !isCreating.value
}
const newBook = ref({
  title: "",
  author: "",
  chapter: "",
  imageUrl: "",
})
const books = ref([])

const createBook = () => {
  const newId = books.value.length + 1
  books.value.push(newBook.value)
}
const handleCreate = () => {
  toggleCreate()
  createModal.showModal()
}
console.log(books.value)
</script>

<template>
  <div class="">
    <div class="mt-10">
      <div class="ml-3 font-bold text-xl">รายการที่คั่นไว้</div>
      <div class="border-b border-gray-500 w-full mt-2"></div>
      <div class="mx-3">
        <div class="flex justify-between items-center mt-5">
          <p>จำนวนทั้งหมด: {{ books.length }}</p>
          <div class="flex space-x-3">
            <button @click="handleCreate" class="btn bg-cyan-300 rounded-3xl">
              Create
            </button>

            <button
              @click="toggleEdit"
              :class="
                isEditing
                  ? 'border-gray-500 text-gray-500'
                  : 'bg-orange-200 text-orange-500 '
              "
              class="btn rounded-3xl px-5"
            >
              <span class="">{{ isEditing ? "ยกเลิก" : "แก้ไข" }}</span>
            </button>
            <button v-if="isEditing" class="btn border-gray-500 rounded-3xl">
              <iconBin class="w-5" />
            </button>
          </div>
        </div>
        <div>
          <div v-for="(book, index) in books" :key="index" class="flex mt-5">
            <img
              :src="books.imageUrl"
              alt=""
              class="w-[100px] h-[150px] rounded-[10px]"
            />
            <div class="ml-3 pr-10">
              <p class="font-bold text-xl">{{ book.title }}</p>
              <p>{{ book.author }}</p>
              <p class="mt-5">{{ book.chapter }}</p>
              <p class="">คั่นล่าสุด: 9 ก.ค.63 / 22.56</p>
            </div>
          </div>
        </div>
        <dialog id="createModal" class="modal modal-bottom sm:modal-middle">
          <div class="modal-box">
            <h3 class="text-lg font-bold">Create your books</h3>
            <div>
              <p class="py-4">Title</p>
              <input v-model="newBook.title" type="text" class="border
              border-gray-500 rounded-3xl p-2 w-full"
            </div>
            <div class="modal-action">
              <form method="dialog">
                <button class="btn">Close</button>
              </form>
            </div>
          </div>
        </dialog>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
