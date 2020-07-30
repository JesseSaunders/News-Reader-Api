<template>
  <div id="app">
    <my-header></my-header>
    <hr />
    <h2>This is my App</h2>
    <router-view></router-view>
    <hr />
    <my-footer></my-footer>
  </div>
</template>

<script>
import MyHeader from "./components/Header.vue";
import MyFooter from "./components/Footer.vue";


export default {
  name: "App",
  components: {
    "my-header": MyHeader,
    "my-footer": MyFooter,
  }
};
</script>

<style>
</style>
