<template>
  <div id="app">
    <nav>
      <ul>
        <li><router-link to="/login">Login</router-link></li>
        <li><router-link to="/signup">Signup</router-link></li>
        <li v-if="isAuthenticated">
          <router-link to="/tasks">Tasks</router-link>
        </li>
        <li v-if="isAuthenticated">
          <a href="#" @click.prevent="logout">Logout</a>
        </li>
      </ul>
    </nav>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  computed: {
    isAuthenticated() {
      return this.$store.state.token !== "";
    },
  },
  methods: {
    logout() {
      this.$store.commit("setToken", "");
      this.$router.push("/login");
    },
  },
};
</script>

<style>
nav {
  margin-bottom: 20px;
}
nav ul {
  list-style-type: none;
  padding: 0;
}
nav ul li {
  display: inline;
  margin-right: 10px;
}
</style>
