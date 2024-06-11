<template>
  <div>
    <h2>Tasks</h2>
    <ul>
      <li v-for="task in tasks" :key="task._id">
        <span
          :style="{ textDecoration: task.completed ? 'line-through' : 'none' }"
        >
          {{ task.description }}
        </span>
        <button @click="completeTask(task._id)" :disabled="task.completed">
          Complete
        </button>
        <button @click="deleteTask(task._id)">Delete</button>
      </li>
    </ul>
    <task-form @task-added="fetchTasks"></task-form>
  </div>
</template>

<script>
import axios from "axios";
import TaskForm from "./TaskForm.vue";

export default {
  components: { TaskForm },
  data() {
    return {
      tasks: [],
    };
  },
  async created() {
    this.fetchTasks();
  },
  methods: {
    async fetchTasks() {
      const token = this.$store.state.token;
      const response = await axios.get("http://localhost:3000/tasks", {
        headers: { Authorization: `Bearer ${token}` },
      });
      this.tasks = response.data;
    },
    async deleteTask(taskId) {
      const token = this.$store.state.token;
      await axios.delete(`http://localhost:3000/tasks/${taskId}`, {
        headers: { Authorization: `Bearer ${token}` },
      });
      this.fetchTasks();
    },
    async completeTask(taskId) {
      const token = this.$store.state.token;
      await axios.patch(
        `http://localhost:3000/tasks/${taskId}/complete`,
        {},
        {
          headers: { Authorization: `Bearer ${token}` },
        }
      );
      this.fetchTasks();
    },
  },
};
</script>
