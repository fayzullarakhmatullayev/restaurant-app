<template>
  <div class="sign-up">
    <img
      src="https://mir-s3-cdn-cf.behance.net/project_modules/disp/cad72f16211207.562a6e3bb04cc.png"
      alt="cad72f16211207"
      class="logo-img"
    />
    <h1 class="sign-title">Login</h1>
    <form class="sign" @submit.prevent="submitHandler">
      <input type="email" v-model.trim="user.email" placeholder="Enter Email" />
      <input
        type="password"
        v-model.trim="user.password"
        placeholder="Enter Password"
      />
      <button>Login</button>
    </form>
    <div class="links">
      <span>Don't have an account? </span
      ><router-link to="/signup">Sign Up</router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      user: {
        email: "",
        password: "",
      },
    };
  },
  methods: {
    async submitHandler() {
      if (this.user.email !== "" && this.user.password !== "") {
        const res = await axios.get(
          `http://localhost:3000/users?email=${this.user.email}&password=${this.user.password}`
        );
        if (res.status === 200 && res.data.length > 0) {
          localStorage.setItem("user_restaurant", JSON.stringify(res.data[0]));
          this.$router.push("/");
        }
      } else {
        alert("All the fields are required to be filled");
      }
    },
  },
  mounted() {
    const user = localStorage.getItem("user_restaurant");
    if (user) {
      this.$router.push("/");
    }
  },
};
</script>

<style></style>
