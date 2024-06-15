<script setup lang="ts">
import { ref, computed } from 'vue'

interface Task {
  name: string
  isfinished: boolean
}
const newTaskName = ref('')
const isShownFinishTasks = ref(false)

const tasks = ref<Task[]>([])
const notFinishedTasks = computed(() => tasks.value.filter((task) => !task.isfinished))
const finishedTasks = computed(() => tasks.value.filter((task) => task.isfinished))

const addTask = () => {
  if(newTaskName.value === '')return
  tasks.value.push({ name: newTaskName.value, isfinished: false })
  newTaskName.value = ''
}
</script>

<template>
  <div>
    <h2>ToDoList</h2>
    <ul>
      <li v-for="(task, index) in notFinishedTasks" :key="task.name">
        {{ index }}: {{ task.name }}
        <button @click="task.isfinished = true">DONE!</button>
      </li>
    </ul>
    <div>
      <label>
        タスク追加
        <input v-model="newTaskName" type="text">
      </label>
      <button @click="addTask">追加</button>
    </div>

    <div v-if="isShownFinishTasks">
      <button @click="isShownFinishTasks=false">完了済みタスクを隠す</button>
      <h3>完了済みタスク</h3>
      <ul>
        <li v-for="(task, index) in finishedTasks" :key="task.name">
          {{ index }}: {{ task.name }}
        </li>
      </ul>
    </div>
    <div v-if="!isShownFinishTasks">
      <button @click="isShownFinishTasks=true">完了済みタスクを表示</button>
    </div>
  </div>
</template>
