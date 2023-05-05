<template>
  <main>
    <header>
      <img src="./assets/logo.svg" alt="" />
      <h1>Pinia Tasks</h1>
    </header>

    <!-- New Task Form -->
    <div class="new-task-form">
      <TaskForm />
    </div>

    <div class="loading" v-if="taskStore.loading">Loading tasks...</div>

    <!-- FILTER -->
    <nav class="filter">
      <button @click="taskStatus = 'all'">All tasks</button>
      <button @click="taskStatus = 'favs'">Fav tasks</button>
    </nav>
    <!-- ALL TASKS -->
    <div class="task-list" v-if="taskStatus === 'all'">
      <p>You have {{ taskStore.totalAmount }} tasks left to be done</p>
      <div v-for="task in taskStore.tasks">
        <TaskDetails :task="task" />
      </div>
    </div>
    <!-- FAV TASKS -->
    <div class="task-list" v-if="taskStatus === 'favs'">
      <p>You have {{ taskStore.favsCount }} fav tasks left to do</p>
      <div v-for="task in taskStore.favs">
        <TaskDetails :task="task" />
      </div>
    </div>
  </main>
</template>

<script>
import { useTaskStore } from "./stores/TaskStore";
import TaskDetails from "./components/TaskDetails.vue";
import { ref } from "vue";
import TaskForm from "./components/TaskForm.vue";
export default {
  components: { TaskDetails, TaskForm },
  setup() {
    const taskStatus = ref("all");
    const taskStore = useTaskStore();
    taskStore.getTasks();
    return { taskStore, taskStatus };
  },
};
</script>
