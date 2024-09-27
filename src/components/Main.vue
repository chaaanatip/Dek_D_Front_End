<script setup>
import { ref } from "vue"
import iconBin from "../components/icons/IconBin.vue"
import IconList from "./icons/IconList.vue"
import IconBookmark from "./icons/IconBookmark.vue"

const date = new Date().toLocaleDateString("th-TH", {
  year: "2-digit",
  month: "short",
  day: "numeric",
})
const time = new Date().toLocaleTimeString("th-TH", {
  hour: "2-digit",
  minute: "2-digit",
})
console.log(time)

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

const selectBooks = ref([null])
const books = ref([])

const createBook = () => {
  const book = { ...newBook.value }

  books.value.push(book)
  newBook.value = {
    title: "",
    author: "",
    chapter: "",
    imageUrl: "",
  }
  createModal.close()
}
const cancelCreate = () => {
  createModal.close()
}

const handleCreate = () => {
  toggleCreate()
  createModal.showModal()
}
</script>

<template>
  <div class="mt-10">
    <div class="ml-3 font-bold text-xl">รายการที่คั่นไว้</div>
    <div class="border-b border-gray-300 w-full mt-2"></div>
    <div class="mx-3">
      <div class="flex justify-between items-center mt-5">
        <p>จำนวนทั้งหมด: {{ books.length }}</p>
        <div class="flex space-x-3">
          <button @click="handleCreate" class="btn bg-cyan-300 rounded-3xl">
            สร้างหนังสือ
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
          <button
            v-if="isEditing && selectBooks !== null"
            class="btn border-gray-500 rounded-3xl"
          >
            <iconBin class="w-5" />
          </button>
        </div>
      </div>
      <div>
        <div v-for="(book, index) in books" :key="index" class="flex mt-5">
          <img
            :src="book.imageUrl"
            alt=""
            class="w-[100px] h-[150px] rounded-[10px]"
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
              <p class="ml-2 flex mb-1">
                คั่นล่าสุด {{ date }} / {{ time }} น.
              </p>
            </div>
          </div>
        </div>
      </div>
      <dialog id="createModal" class="modal modal-bottom sm:modal-middle">
        <div class="modal-box">
          <form method="dialog" class="space-x-2" @submit.prevent="createBook">
            <h3 class="text-lg font-bold mb-5">Create your books</h3>
            <div class="items-center space-y-2">
              <h1>Title</h1>
              <input
                v-model="newBook.title"
                type="text"
                class="pl-5 border border-gray-500 p-2 w-full rounded-md"
                required
              />
              <h1>Author</h1>
              <input
                v-model="newBook.author"
                type="text"
                class="pl-5 border border-gray-500 p-2 w-full rounded-md"
                required
              />
              <h1>Chapter</h1>
              <input
                v-model="newBook.chapter"
                type="text"
                class="pl-5 border border-gray-500 p-2 w-full rounded-md"
                required
              />
              <h1>ImageUrl</h1>
              <input
                v-model="newBook.imageUrl"
                type="url"
                class="pl-5 border border-gray-500 p-2 w-full rounded-md"
                required
              />
            </div>

            <div class="modal-action">
              <button class="btn bg-cyan-400 text-white" type="submit">
                Submit
              </button>
              <button
                class="btn bg-gray-400 text-white"
                type="button"
                @click="cancelCreate"
              >
                Cancel
              </button>
            </div>
          </form>
        </div>
      </dialog>
    </div>
  </div>
</template>

<style scoped></style>
