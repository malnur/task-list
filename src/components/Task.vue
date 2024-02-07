<script setup>
import { ref, computed } from 'vue'
import { Switch } from '@headlessui/vue'
import Modal from './Modal.vue'

const props = defineProps(['task', 'removeTask'])
const emit = defineEmits(['remove-task', 'toggle-task'])

const enabled = computed(() => props.task.completed)

const remove = (event) => {
  emit('remove-task', event)
}

const toggle = (event) => {
  emit('toggle-task', event)
}

const modal = ref(null)

const openModal = () => {
  modal.value.openModal()
}
</script>

<template>
  <hr />
  <div class="flex my-2">
    <div class="self-center ml-2 mr-4">
      <Switch
        :class="enabled ? 'bg-emerald-200' : 'bg-gray-100'"
        class="relative inline-flex h-6 w-11 items-center rounded-full"
        :title="props.task.id"
        @click="toggle"
      >
        <span class="sr-only">Enable notifications</span>
        <span
          :class="enabled ? 'translate-x-6' : 'translate-x-1'"
          class="inline-block h-4 w-4 transform rounded-full bg-white transition"
        />
      </Switch>
    </div>
    <div class="basis-3/4">
      <h3 class="text-xl" :class="{ [`text-emerald-400`]: enabled }">{{ props.task.title }}</h3>
      <p class="text-gray-500">{{ props.task.description }}</p>
    </div>
    <button
      type="button"
      class="self-center text-sm font-bold tracking-wide bg-rose-400 text-gray-50 p-2 h-9 rounded-lg focus:outline-none focus:shadow-outline"
      :title="props.task.id"
      @click="remove"
    >
      Delete
    </button>
    <button
      type="button"
      class="self-center text-sm font-bold tracking-wide bg-emerald-200 text-gray-500 ml-2 p-2 h-9 rounded-lg focus:outline-none focus:shadow-outline"
      :title="props.task.id"
      @click="openModal"
    >
      Details
    </button>
  </div>
  <Modal ref="modal">{{ props.task.description }}</Modal>
</template>
