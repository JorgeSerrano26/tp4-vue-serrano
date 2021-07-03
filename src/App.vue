<template>
  <div id="app" class="container-fluid my-3">
    <div class="jumbotron">
      <h1>tp4 vue serrano</h1>
      <Navbar />
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
import Navbar from "./components/Navbar";
export default {
  name: "App",
  components: {
    Navbar,
  },
};
</script>

<style>
.jumbotron {
  padding: 20px;
}
</style>
