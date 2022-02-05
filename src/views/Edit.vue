<template>
  <the-header />
  <div class="container">
    <h1 class="title">{{ name }}, you can update the restaurant here</h1>
    <div class="loading" v-if="isLoading">Loading...</div>
    <form class="sign" @submit.prevent="submitHandler" v-else>
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
      <button>Update the Restaurant</button>
    </form>
  </div>
</template>

<script>
import TheHeader from "../components/TheHeader.vue";
import axios from "axios";
export default {
  name: "Edit",
  components: { TheHeader },
  data() {
    return {
      name: JSON.parse(localStorage.getItem("user")).name,
      restuarant: {
        name: "",
        contact: "",
        address: "",
      },
      isLoading: false,
    };
  },
  methods: {
    async submitHandler() {
      if (
        this.restuarant.name !== "" &&
        this.restuarant.contact !== "" &&
        this.restuarant.address !== ""
      ) {
        await axios.put(
          `http://localhost:3000/restaurants/${this.$route.params.id}`,
          {
            name: this.restuarant.name,
            contact: this.restuarant.contact,
            address: this.restuarant.address,
          }
        );
        alert("The restaurant successfully has been updated");
        this.$router.push("/");
      } else {
        alert("All the fields are required to be filled");
      }
    },
  },
  async mounted() {
    const user = localStorage.getItem("user");
    if (!user) {
      this.$router.push("/signup");
    }
    this.isLoading = true;
    const { data } = await axios.get(
      `http://localhost:3000/restaurants/${this.$route.params.id}`
    );
    this.restuarant = data;
    this.isLoading = false;
  },
};
</script>
