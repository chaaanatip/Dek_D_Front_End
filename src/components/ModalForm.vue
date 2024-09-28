<!-- ModalForm.vue -->
<script setup>
import { ref, defineEmits } from "vue"

const emit = defineEmits()

const newBook = ref({
  title: "",
  author: "",
  chapter: "",
  imageUrl: "",
})

const createBook = () => {
  emit("create", { ...newBook.value })
  newBook.value = {
    title: "",
    author: "",
    chapter: "",
    imageUrl: "",
  }
}

const cancelCreate = () => {
  emit("cancel")
}
</script>

<template>
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
</template>

<style scoped></style>
