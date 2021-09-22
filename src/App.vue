<template>
  <NavBar />
  <router-view />
</template>

<script>
import NavBar from "./components/NavBar.vue";

export default {
  components: {
    NavBar,
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Spartan:wght@400;600;700&display=swap");

body {
  background-color: #141625;
  overflow-x: hidden;
}

#app {
  font-family: "spartan", Arial, sans-serif;
  max-width: 600px;
  margin: 0 auto;
}
</style>
