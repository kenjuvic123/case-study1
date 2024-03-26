<template>
  <div>
    <WelcomeItem>
      <template #icon>
        <DocumentationIcon />
      </template>
      <div class="title">Task List:</div>
      <div class="flex items-center">
        <input
          type="text"
          v-model="taskInput"
          placeholder="Add task"
          class="ml-2 mr-2 input-field"
        />
        <button @click="handleButtonClick" class="btn">➕</button>
      </div>
      <template #heading> </template>
    </WelcomeItem>
    <!-- test -->
    <ul class="task-list">
      <li v-for="(task, index) in tasks" :key="index">
        <input type="checkbox" v-model="task.completed" class="checkbox" />
        <span>{{ task.description }}</span>
        <button @click="removeTask(index)" class="btn-delete">❌</button>
        <button @click="editTask(index)" class="btn-edit">✏️</button>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import WelcomeItem from './WelcomeItem.vue'
import DocumentationIcon from './icons/IconDocumentation.vue'
import { ref, onMounted } from 'vue'

interface Task {
  id: number
  description: string
  completed: boolean
}

const taskInput = ref('')
const tasks = ref<Task[]>([])

// Load tasks from localStorage on component mount
onMounted(() => {
  const storedTasks = localStorage.getItem('tasks')
  if (storedTasks) {
    tasks.value = JSON.parse(storedTasks)
  }
})

const handleButtonClick = () => {
  if (taskInput.value.trim() !== '') {
    tasks.value.push({ id: tasks.value.length + 1, description: taskInput.value, completed: false })
    taskInput.value = ''
    saveTasksToLocalStorage()
  }
}

const saveTasksToLocalStorage = () => {
  localStorage.setItem('tasks', JSON.stringify(tasks.value))
}

const removeTask = (index: number) => {
  tasks.value.splice(index, 1)
  saveTasksToLocalStorage()
}

const editTask = (index: number) => {
  const newDescription = prompt('Enter new description for task:')
  if (newDescription !== null) {
    tasks.value[index].description = newDescription
    saveTasksToLocalStorage()
  }
}
</script>

<style scoped>
/* Add this style to remove the bullet points */
.task-list {
  padding-left: 95px;
  list-style: none; /* Remove bullet points */
}

/* Rest of your existing styles */
.btn {
  background-color: #3490dc;
  color: #fff;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 0.25rem;
  cursor: pointer;
  margin-left: 1rem;
}

.btn:hover {
  background-color: #2779bd;
}

.input-field {
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 0.25rem;
  flex-grow: 1;
}

.btn-delete {
  margin-left: 9rem;
}

.title {
  font-size: 1.2rem;
  margin-bottom: 0.5rem;
}

.checkbox {
  margin-right: 0.5rem;
}
</style>
