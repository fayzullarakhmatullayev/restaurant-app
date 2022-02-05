<template>
  <the-header />
  <div class="container">
    <h1 class="title">{{ name }}, you can add a new restaurant here</h1>
    <form class="sign" @submit.prevent="submitHandler">
      <input type="text" v-model="restuarant.name" placeholder="Enter Name" />
      <input
        type="text"
        v-model="restuarant.address"
        placeholder="Enter Address"
      />
      <input
        type="text"
        v-model="restuarant.contact"
        placeholder="Enter Contact"
      />
      <button>Add new Restaurant</button>
    </form>
  </div>
</template>

<script>
import TheHeader from "../components/TheHeader.vue";
import axios from "axios";
export default {
  name: "Add",
  components: { TheHeader },
  data() {
    return {
      name: JSON.parse(localStorage.getItem("user")).name,
      restuarant: {
        name: "",
        contact: "",
        address: "",
      },
    };
  },
  methods: {
    async submitHandler() {
      if (
        this.restuarant.name !== "" &&
        this.restuarant.contact !== "" &&
        this.restuarant.address !== ""
      ) {
        const res = await axios.post("http://localhost:3000/restaurants", {
          name: this.restuarant.name,
          contact: this.restuarant.contact,
          address: this.restuarant.address,
        });
        alert("Restaurant successfully has been created!");
        this.$router.push("/");
      } else {
        alert("All the fields are required to be filled");
      }
    },
  },
  mounted() {
    const user = localStorage.getItem("user");
    if (!user) {
      this.$router.push("/signup");
    }
  },
};
</script>
