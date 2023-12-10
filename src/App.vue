<template>
  <CoffeeShop msg="Welcome to Your Coffee Shop" />
</template>

<script>
import CoffeeShop from "./components/CoffeeShop.vue";

export default {
  name: "App",
  components: {
    CoffeeShop,
  },
};
</script>

<style>
body {
  background-color: black;
  margin: 0;
  overflow-x: hidden;
  overflow-y: scroll;
  box-sizing: border-box;
}
body::-webkit-scrollbar {
  width: 5px;
}

body::-webkit-scrollbar-thumb {
  background: #7e7e7e;
  border-radius: 50px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
