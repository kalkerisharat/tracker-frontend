<template>
  <div>
    <h2>Signup</h2>
    <form @submit.prevent="signup">
      <input v-model="username" type="text" placeholder="Username" required />
      <input
        v-model="password"
        type="password"
        placeholder="Password"
        required
      />
      <input
        v-model="confirmPassword"
        type="password"
        placeholder="Confirm Password"
        required
      />
      <button type="submit">Signup</button>
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
      confirmPassword: "",
    };
  },
  methods: {
    async signup() {
      if (this.password !== this.confirmPassword) {
        return alert("Passwords do not match");
      }
      try {
        await axios.post("http://localhost:3000/auth/signup", {
          username: this.username,
          password: this.password,
        });
        this.$router.push("/login");
      } catch (error) {
        console.error("Signup failed", error);
      }
    },
  },
};
</script>
