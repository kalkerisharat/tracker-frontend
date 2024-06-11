<template>
  <div>
    <h3>Add Task</h3>
    <form @submit.prevent="addTask">
      <input
        v-model="description"
        type="text"
        placeholder="Task description"
        required
      />
      <button type="submit">Add Task</button>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      description: "",
    };
  },
  methods: {
    async addTask() {
      const token = this.$store.state.token;
      await axios.post(
        "http://localhost:3000/tasks",
        {
          description: this.description,
        },
        {
          headers: { Authorization: `Bearer ${token}` },
        }
      );
      this.$emit("task-added");
      this.description = "";
    },
  },
};
</script>
