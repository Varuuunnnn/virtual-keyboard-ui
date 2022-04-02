<template>
  <div id="app">
    <h3>{{ applicationName }}</h3>
    <Keyboard />
  </div>
</template>

<script>
import Keyboard from "./components/Keyboard.vue";
const applicationName = "Virtual Keyboard";
export default {
  name: "App",
  components: {
    Keyboard
  },
  data() {
    return {
      applicationName
    };
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
