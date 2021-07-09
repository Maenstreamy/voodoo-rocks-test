<template>
  <div id="app">
    <posts />
  </div>
</template>

<script>
import Posts from "./components/Posts.vue";

export default {
  name: "App",
  components: {
    Posts,
  },
};
</script>

<style lang="scss">
@import url("./normalize.css");
body {
  background-color: #f0f8ff;
}
h2 {
  margin: 0;
}
p {
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  max-width: 1920px;
  margin: 0 auto;
  padding: 20px;
}
</style>
