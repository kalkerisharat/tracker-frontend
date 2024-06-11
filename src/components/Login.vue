<template>
  <div>
    <h2>Login</h2>
    <form @submit.prevent="login">
      <input v-model="username" type="text" placeholder="Username" required />
      <input
        v-model="password"
        type="password"
        placeholder="Password"
        required
      />
      <button type="submit">Login</button>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    async login() {
      try {
        const response = await axios.post("http://localhost:3000/auth/login", {
          username: this.username,
          password: this.password,
        });
        this.$store.commit("setToken", response.data.token);
        this.$router.push("/tasks");
      } catch (error) {
        console.error("Login failed", error);
      }
    },
  },
};
</script>
