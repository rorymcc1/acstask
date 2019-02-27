<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <testList msg="Welcome to ACS Code Challenge using Vue.js" />
  </div>
</template>

<script>
import testList from "./components/testList.vue";

export default {
  name: "app",
  components: {
    testList
  }
};
</script>

