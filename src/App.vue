<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>

export default {
  name: "App",
  components: {
  },
  data() {
    return {
    };
  }
};
</script>

<style lang="scss">
@import "./assets/lib/reset.css";
@import url("https://fonts.googleapis.com/css?family=Roboto:100,100i,300,300i,400,400i,500,500i,700,700i,900,900i&display=swap&subset=cyrillic,cyrillic-ext");
body {
  font-family: "Roboto", sans-serif;
}
</style>
