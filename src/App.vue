<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Timesheet msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import Timesheet from './components/Timesheet.vue'

export default {
  name: 'app',
  components: {
    Timesheet
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
}
</style>
