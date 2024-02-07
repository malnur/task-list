<script setup>
import Task from './Task.vue'

const props = defineProps(['tasks'])
const emit = defineEmits(['remove-task', 'toggle-complete-task'])

const removeTask = (event) => {
  emit('remove-task', event.target.title)
}

const toggleTaskStatus = (event) => {
  emit('toggle-complete-task', event.target.title)
}
</script>

<template>
  <div>
    <ul>
      <li v-for="task in props.tasks" :key="task.id">
        <Task :task="task" @remove-task="removeTask" @toggle-task="toggleTaskStatus" />
      </li>
    </ul>
  </div>
</template>
