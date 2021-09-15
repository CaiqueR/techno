<template>
  <div id="app">
    <Main />
  </div>
</template>

<script>
import Main from "./components/Main.vue";

export default {
  components: { Main },
  name: "App",
};
</script>

<style>
#app {
  padding: 0 80px;
}

* {
  padding: 0px;
  margin: 0px;
  box-sizing: border-box;
}

body {
  background: linear-gradient(to right, #1a1a1a 30%, #ffffff 30%);
  font-family: "Noto Serif", serif;
}

ul {
  list-style: none;
}
</style>
