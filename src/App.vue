<template>
  <main>
    <!-- heading -->
    <header>
      <img src="./assets/pinia-logo.svg" alt="pinia logo" />
      <h1>Pinia Tasks</h1>
    </header>

    <!-- new task form -->
    <div class="new-task-form">
      <TaskForm />
    </div>

    <!-- filter -->
    <nav class="filter">
      <button @click="filter = 'all'">All tasks</button>
      <button @click="filter = 'favs'">Fav tasks</button>
    </nav>

    <!-- loading -->
    <div class="loading" v-if="TaskStore.loading">Loading tasks...</div>

    <!-- task list -->
    <div class="task-list" v-if="filter === 'all'">
      <p>You have {{ TaskStore.totalCount }} tasks left to do</p>
      <div v-for="task in TaskStore.tasks">
        <TaskDetails :task="task" />
      </div>
    </div>
    <!-- favs list -->
    <div class="task-list" v-if="filter === 'favs'">
      <p>You have {{ TaskStore.favCount }} tasks left to do</p>
      <div v-for="task in TaskStore.favs">
        <TaskDetails :task="task" />
      </div>
    </div>
  </main>
</template>

<script setup>
import { ref } from 'vue'
import { useTaskStore } from './stores/TaskStore'
import TaskDetails from './components/TaskDetails.vue'
import TaskForm from './components/TaskForm.vue'

const TaskStore = useTaskStore()

// fetch tasks
TaskStore.getTasks()

const filter = ref('all')
</script>
