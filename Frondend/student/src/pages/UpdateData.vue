<template>
  <div>
    <BennerImage></BennerImage>
    <FormUpdate></FormUpdate>
    <Footer></Footer>
  </div>
</template>

<script>
import BennerImage from "@/components/BennerImage.vue";
import FormUpdate from "@/components/FormUpdate.vue";
import Footer from "@/components/Footer.vue";

export default {
  name: "UpdateData",
  components: {
    BennerImage,
    FormUpdate,
    Footer,
  },
};
</script>

<style>

</style>