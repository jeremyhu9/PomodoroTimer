<template>
  <div id="app">
    <Landing></Landing>
  </div>
</template>

<script>
import Landing from './components/Landing'
import '../src/assets/styles.css'

export default {
  name: 'app',
  components: {
    Landing
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
  margin-top: 60px;
}
</style>
