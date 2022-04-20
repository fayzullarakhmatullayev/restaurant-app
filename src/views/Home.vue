<template>
  <the-header />
  <div class="container">
    <h1 class="title">Hello {{ name }}, Welcome to Home Page</h1>
    <div class="loading" v-if="!restaurans.length">Loading...</div>
    <table class="table" v-else>
      <thead>
        <tr>
          <th>#</th>
          <th>Name</th>
          <th>Contact</th>
          <th>Address</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(res, index) in restaurans" :key="res.id">
          <td>{{ index + 1 }}</td>
          <td>{{ res.name }}</td>
          <td>{{ res.contact }}</td>
          <td>{{ res.address }}</td>
          <td>
            <router-link :to="`/update/${res.id}`">Update</router-link>,
            <a href="#" @click.prevent="deleteRestaurant(res.id)">Delete</a>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";
import TheHeader from "../components/TheHeader.vue";
export default {
  name: "Home",
  components: { TheHeader },
  data() {
    return {
      name: JSON.parse(localStorage.getItem("user_restaurant")).name,
      restaurans: [],
    };
  },
  methods: {
    async deleteRestaurant(id) {
      const isOk = confirm("Are you sure to delete this restaurant?");
      if (isOk) {
        await axios.delete(`http://localhost:3000/restaurants/${id}`);
        await this.loadData();
      }
    },
    async loadData() {
      const user = localStorage.getItem("user_restaurant");
      if (!user) {
        this.$router.push("/signup");
      }

      const { data } = await axios.get("http://localhost:3000/restaurants");
      this.restaurans = data;
    },
  },
  async mounted() {
    await this.loadData();
  },
};
</script>
