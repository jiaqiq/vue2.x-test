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
 
}
</style>
