<template>
  <header class="header">
    <div class="container">
      <div class="header-nav">
        <ul class="header-menu">
          <li>
            <router-link class="link" to="/">Home</router-link>
          </li>
          <li>
            <router-link class="link" to="/add">Add Restaurant</router-link>
          </li>
        </ul>
        <a @click.prevent="logout" class="link" href="#">Logout</a>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  methods: {
    logout() {
      localStorage.removeItem("user_restaurant");
      this.$router.push("/login");
    },
  },
};
</script>

<style></style>
