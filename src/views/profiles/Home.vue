<template>
  <div class="home">
    <!--img alt="Vue logo" src="../assets/logo.png">-->
    <Slider />
    <hr class="my-3" />
<center><h1> SELAMAT DATANG DI PROFILE DIRI </h1></center>
  </div>
</template>

<script>
import Slider from "@/components/Slider.vue";

export default {
  name: "Home",
  components: {
    Slider,
  },
};
</script>