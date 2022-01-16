<template>
  <div id="App">
    <Landing />
  </div>
</template>

<script>
import Landing from "./pages/Landing.vue";
export default {
  name: "App",
  components: {
    Landing,
  },
};
</script>

<style lang="scss">
  body{
    margin: 0;
    font-family: 'Poppins';
  }
</style>
