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
            <button @click="toggleCreate" class="btn bg-cyan-300 rounded-3xl">
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
          <div class="flex mt-5">
            <img
              src="https://img.freepik.com/free-vector/paper-branding-mockup-vector-set_53876-62032.jpg?w=826&t=st=1727369100~exp=1727369700~hmac=2574660bbd30809193ba104a4b929c8b7e8a18faacdc169710077c9fde0709a7"
              alt=""
              class="w-[100px] h-[150px] rounded-[10px]"
            />
            <div class="ml-3 pr-10">
              <p class="font-bold text-xl">
                นิยายขายดีโดเรม่อน อิอิฟหกดฟหกดฟหกดฟหกด
              </p>
              <p>G.lina</p>
              <p class="mt-5">ตอนที่1: ไฟฉายย่อส่วน</p>
              <p class="">คั่นล่าสุด 9 ก.ค.63 / 22.56</p>
            </div>
          </div>
          <div class="flex mt-5">
            <img
              src="https://img.freepik.com/free-vector/paper-branding-mockup-vector-set_53876-62032.jpg?w=826&t=st=1727369100~exp=1727369700~hmac=2574660bbd30809193ba104a4b929c8b7e8a18faacdc169710077c9fde0709a7"
              alt=""
              class="w-[100px] h-[150px] rounded-[10px]"
            />
            <div class="ml-3 pr-10">
              <p class="font-bold text-xl">
                นิยายขายดีโดเรม่อน อิอิฟหกดฟหกดฟหกดฟหกด
              </p>
              <p>G.lina</p>
              <p class="mt-5">ตอนที่1: ไฟฉายย่อส่วน</p>
              <p class="">คั่นล่าสุด 9 ก.ค.63 / 22.56</p>
            </div>
          </div>
          <div class="flex mt-5">
            <img
              src="https://img.freepik.com/free-vector/paper-branding-mockup-vector-set_53876-62032.jpg?w=826&t=st=1727369100~exp=1727369700~hmac=2574660bbd30809193ba104a4b929c8b7e8a18faacdc169710077c9fde0709a7"
              alt=""
              class="w-[100px] h-[150px] rounded-[10px]"
            />
            <div class="ml-3 pr-10">
              <p class="font-bold text-xl">
                นิยายขายดีโดเรม่อน อิอิฟหกดฟหกดฟหกดฟหกด
              </p>
              <p>G.lina</p>
              <p class="mt-5">ตอนที่1: ไฟฉายย่อส่วน</p>
              <p class="">คั่นล่าสุด 9 ก.ค.63 / 22.56</p>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div
      v-if="isCreating"
      class="fixed inset-0 bg-gray-500 bg-opacity-75 flex items-center justify-center z-50"
    >
      <div class="bg-white p-6 rounded-lg w-96">
        <h2 class="text-lg font-bold mb-4">เพิ่มนิยายใหม่</h2>
        <form @submit.prevent="createBook">
          <div class="mb-4">
            <label class="block text-sm font-medium mb-2">ชื่อเรื่อง</label>
            <input
              type="text"
              v-model="newBook.title"
              class="border rounded w-full px-3 py-2"
              required
            />
          </div>
          <div class="mb-4">
            <label class="block text-sm font-medium mb-2">ชื่อนักเขียน</label>
            <input
              type="text"
              v-model="newBook.author"
              class="border rounded w-full px-3 py-2"
              required
            />
          </div>
          <div class="mb-4">
            <label class="block text-sm font-medium mb-2">ชื่อตอน</label>
            <input
              type="text"
              v-model="newBook.chapter"
              class="border rounded w-full px-3 py-2"
              required
            />
          </div>
          <div class="mb-4">
            <label class="block text-sm font-medium mb-2">ลิงก์ภาพ</label>
            <input
              type="text"
              v-model="newBook.imageUrl"
              class="border rounded w-full px-3 py-2"
              required
            />
          </div>
          <div class="flex justify-end">
            <button
              type="button"
              @click="toggleCreate"
              class="mr-2 text-gray-500"
            >
              ยกเลิก
            </button>
            <button
              type="submit"
              class="bg-green-500 text-white rounded px-4 py-2"
            >
              เพิ่ม
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
