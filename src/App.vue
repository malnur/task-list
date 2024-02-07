<script setup>
import { ref, computed } from 'vue'
import Data from './components/Data.vue'
import TaskList from './components/TaskList.vue'
import TextForm from './components/TaskForm.vue'

import TasksIcon from './components/icons/tasks.svg'
import CompletedIcon from './components/icons/completed.svg'

const data = ref(null)
const totalTasks = computed(() => data.value?.tasks.length)
const completedTasks = computed(() => data.value?.tasks.filter((task) => task.completed).length)
</script>

<template>
  <Data ref="data" />

  <div class="container m-auto min-h-screen w-full bg-white pt-9">
    <div class="flex h-full">
      <aside class="flex flex-col w-[30%] min-w-48">
        <div class="flex justify-around">
          <div class="flex justify-between p-3 basis-1/2 h-24 rounded-lg bg-gray-300">
            <div class="text-center">
              <div class="w-8 h-8 rounded-full bg-gray-500">
                <img class="w-6 m-auto pt-1 filter-white" :src="TasksIcon" alt="all tasks" />
              </div>
              <div class="mt-3 font-semibold text-gray-500">All</div>
            </div>
            <div class="self-start font-semibold text-2xl text-gray-500">{{ totalTasks }}</div>
          </div>
          <div class="flex justify-between p-3 basis-1/3 h-24 rounded-lg bg-emerald-200">
            <div class="text-center">
              <div class="w-8 h-8 rounded-full bg-gray-500">
                <img class="w-6 m-auto pt-1 filter-white" :src="CompletedIcon" alt="all tasks" />
              </div>
              <div class="mt-3 font-semibold text-gray-500">Completed</div>
            </div>
            <div class="self-start font-semibold text-2xl text-gray-500">{{ completedTasks }}</div>
          </div>
        </div>
        <TextForm @addTask="data?.addTask" />
      </aside>
      <div class="flex flex-col w-full px-4">
        <header>
          <h1 class="my-8 text-3xl font-bold text-amber-600">Task List</h1>
        </header>
        <TaskList
          :tasks="data?.tasks"
          @remove-task="data?.removeTask"
          @toggle-complete-task="data?.toggleCompleteTask"
        />
      </div>
    </div>
  </div>
</template>

<style>
.filter-white {
  filter: invert(100%) sepia(100%) saturate(0%) hue-rotate(119deg) brightness(104%) contrast(102%);
}
</style>
