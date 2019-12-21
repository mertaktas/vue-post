<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <PostComponent />
  </div>
</template>

<script>
import PostComponent from "./components/PostComponent.vue";

export default {
  name: "app",
  components: {
    PostComponent
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 10px;
}
</style>
