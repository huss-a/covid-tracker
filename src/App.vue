<template>
  <Header />
  <div class="container">
    <Home/>
  </div>
</template>

<script lang="ts">
import Header from "./components/Header.vue";
import Home from "@/components/Home"

export default {
  components: {
    Header,
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Rubik:ital,wght@0,300;0,400;0,500;1,300;1,400&display=swap");
</style>
