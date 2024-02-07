<script setup>
import { ref } from 'vue'

const emit = defineEmits(['addTask'])

const title = ref('')
const description = ref('')

const newTask = () => {
  if (title.value) {
    const item = {}
    item.title = title.value
    item.description = description.value
    emit('addTask', item)
  }

  title.value = ''
  description.value = ''
}
</script>

<template>
  <div class="m-6">
    <input
      class="w-full bg-gray-100 text-gray-900 mt-2 p-3 rounded-lg focus:outline-none focus:shadow-outline"
      type="text"
      required
      placeholder="Title *"
      v-model="title"
    />
    <div class="my-2">
      <textarea
        placeholder="Description"
        class="w-full h-32 bg-gray-100 text-gray-900 mt-2 p-3 rounded-lg focus:outline-none focus:shadow-outline"
        v-model="description"
      ></textarea>
    </div>
    <div class="flex my-2 w-1/2">
      <button
        type="button"
        class="text-sm font-bold tracking-wide bg-emerald-200 text-gray-500 p-2 rounded-lg w-1/2 focus:outline-none focus:shadow-outline"
        @click="newTask"
      >
        Add
      </button>
    </div>
  </div>
</template>
