<template>
  <div>
    <img style="width: 100vw" src="../assets/baner.jpg" alt="" />
    <router-link to="/add" v-show="routLink == '/'">
      <button class="btn btn-primary my-3 ml-3">Add Data</button>
    </router-link>
    <router-link to="/" v-show="routLink == '/add'">
      <button class="btn btn-primary my-3 ml-3">Back</button>
    </router-link>
  </div>
</template>

<script>
export default {
  name: "BennerImage",

  data() {
    return {
      routLink: this.$route.path
    }
  }
};
</script>

<style>

</style>