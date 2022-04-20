<template>
  <div class="sign-up">
    <img
      src="https://mir-s3-cdn-cf.behance.net/project_modules/disp/cad72f16211207.562a6e3bb04cc.png"
      alt="cad72f16211207"
      class="logo-img"
    />
    <h1 class="sign-title">Sign Up</h1>
    <form class="sign" @submit.prevent="submitHandler">
      <input type="text" v-model.trim="user.name" placeholder="Enter Name" />
      <input type="email" v-model.trim="user.email" placeholder="Enter Email" />
      <input
        type="password"
        v-model.trim="user.password"
        placeholder="Enter Password"
      />
      <button>Sign Up</button>
    </form>
    <div class="links">
      <span>Already have an account? </span
      ><router-link to="/login">Login</router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      user: {
        name: "",
        email: "",
        password: "",
      },
    };
  },
  methods: {
    async submitHandler() {
      if (
        this.user.name !== "" &&
        this.user.email !== "" &&
        this.user.password !== ""
      ) {
        const { data } = await axios.post(
          "http://localhost:3000/users",
          this.user
        );

        alert("User has been successfully created");
        localStorage.setItem("user_restaurant", JSON.stringify(data));
        this.user = {
          name: "",
          email: "",
          password: "",
        };
        this.$router.push("/");
      } else {
        alert("All the fields are required to be filled");
      }
    },
  },
  mounted() {
    const user = localStorage.getItem("user");
    if (user) {
      this.$router.push("/");
    }
  },
};
</script>

<style></style>
