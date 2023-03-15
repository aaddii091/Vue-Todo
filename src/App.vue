<template>
  <NavBar />
  <router-view />
</template>
<script>
import NavBar from "../src/components/NavBar.vue";
export default {
  components: { NavBar },
  data() {
    return {};
  },
};
</script>
<style>
body {
  background-color: black;
  font-family: "Roboto", sans-serif;
}
</style>
