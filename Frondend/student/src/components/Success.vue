<template>
  <div class="cards">
    <div class="card-body ">
      <h5 class="card-title">Success!</h5>
      <p class="card-text">Your Data Has Been {{ Judul }} !</p>
      <router-link to="/" v-if="Judul === 'Submit'">
        <button class="back btn btn-primary mt-3">Back</button>
      </router-link>
      <router-link to="/" v-else-if="Judul === 'Update'">
        <button class="back btn btn-primary mt-3">Back</button>
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "SuccesS",
  data() {
    return {
      Judul: null,
    };
  },
  methods: {
    ubahJudul() {
      let route = this.$route.fullPath;
      if (route === "/add") {
        this.Judul = "Submit";
      } else {
        this.Judul = "Update";
      }
    },
  },
  mounted() {
    this.ubahJudul();
  },
};
</script>

<style scoped>
.back {
  margin-left: 9rem;
}

.border-color-pink {
  border: solid 2px #f9cada;
}

.bg-color-pink {
  background-color: #f9cada;
}

.cards {
  border-radius: 10px;
  border: 1px solid blue;
  margin-top: 20px;
  padding-left: 50px;
  padding-right: 50px;
}
</style>