<template>
  <div id="app">
    <Donut/>
  </div>
</template>

<script>
import Donut from "./components/Donut";

export default {
  name: "App",
  components: {
    Donut
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
