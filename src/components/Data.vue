<script setup>
import { ref, reactive } from 'vue'

const tasks = reactive([
  { id: 1, title: 'Wake Up', description: 'To become awake', completed: false },
  { id: 2, title: 'Have Breakfast', description: 'First meal', completed: false },
  { id: 3, title: 'Get Dressed', description: 'Put on clothes', completed: false }
])
const count = ref(4)

const addTask = (newTask) => {
  newTask.id = count.value
  newTask.completed = false
  tasks.push(newTask)
  count.value++
}

const removeTask = (taskId) => {
  const task = tasks.find((element) => element.id == taskId)
  if (task) {
    tasks.splice(task, 1)
  }
}

const toggleCompleteTask = (taskId) => {
  const task = tasks.find((element) => element.id == taskId)
  if (task) {
    task.completed = !task.completed
  }
}

defineExpose({
  tasks,
  addTask,
  removeTask,
  toggleCompleteTask
})
</script>
