<template>
  <router-view />
</template>
<script>
export default {
  beforeCreate() {
    if (localStorage.getItem("user_restaurant")) {
      this.$router.push("/");
    } else {
      this.$router.push("/login");
    }
  },
};
</script>
<style lang="scss"></style>
