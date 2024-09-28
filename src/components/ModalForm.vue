<script setup>
import { ref } from "vue"
const emit = defineEmits(["handleCreate"])
const selectedFile = ref(null)
const newBook = ref({
  title: "",
  author: "",
  chapter: "",
  imageUrl: "",
})

const formModal = ref(null)

const handleFileChange = (event) => {
  selectedFile.value = event.target.files[0]
}

const uploadFile = async () => {
  if (selectedFile.value) {
    const formData = new FormData()
    formData.append("file", selectedFile.value)
    formData.append("uploadType", "0")

    try {
      const response = await fetch("https://up.m1r.ai/upload", {
        method: "POST",
        body: formData,
      })

      if (!response.ok) {
        throw new Error("File upload failed")
      }

      const result = await response.json()
      console.log("Upload successful:", result.url)

      newBook.value.imageUrl = result.url

      createBook()
    } catch (error) {
      console.error("Error uploading file:", error)
    }
  }
}

const createBook = () => {
  console.log("Book created:", newBook.value)
  emit("handleCreate", newBook.value)
  newBook.value = {
    title: "",
    author: "",
    chapter: "",
    imageUrl: "",
  }

  if (formModal.value) {
    formModal.value.close()
  }
}

const cancelCreate = () => {
  if (formModal.value) {
    formModal.value.close()
  }
}
</script>

<template>
  <dialog
    id="createModal"
    class="modal modal-bottom sm:modal-middle"
    ref="formModal"
  >
    <div class="modal-box">
      <form method="dialog" class="space-x-2" @submit.prevent="uploadFile">
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
          <h1>Upload Image</h1>
    
          <input
            type="file"
            @change="handleFileChange"
            class="pl-5 border border-gray-500 p-2 w-full rounded-md"
            accept="image/*"
            required
          />
        </div>

        <div class="modal-action">
          <button class="btn bg-cyan-400 text-white" type="submit">
            Upload and Submit
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
