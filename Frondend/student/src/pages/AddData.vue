<template>
  <div>
    <BennerImage></BennerImage>
    <FormAdd></FormAdd>
    <Success class="d-none"></Success>
    <Footer></Footer>
  </div>
</template>
<script>
import BennerImage from "../components/BennerImage.vue";
import FormAdd from "../components/FormAdd.vue";
import Footer from "../components/Footer.vue";
import Success from "../components/Success.vue";

export default {
  name: "AddData",
  components: {
    BennerImage,
    FormAdd,
    Success,
    Footer,
  },
};
</script>

<style scoped>

</style>>