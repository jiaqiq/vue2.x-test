<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <!-- <Table></Table> -->
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
// import Table from './components/table.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    // Table
  }
}
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
