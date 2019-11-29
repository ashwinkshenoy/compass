<template>
  <div id="app">
    <magnet />
  </div>
</template>

<script>
import Magnet from './components/Magnet.vue'

export default {
  name: 'app',
  components: {
    Magnet
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
  width: 100%;
  overflow-x: hidden;
}
</style>
