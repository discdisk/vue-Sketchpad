<template>

  <div id="app">
    <navBar/>
    <img alt="Vue logo" src="./assets/logo.png">
    <sketchPad user="discdisk"/>
  </div>
</template>

<script>
import sketchPad from './components/sketchPad.vue'
import navBar from './components/navBar.vue'
export default {
  name: 'app',
  components: {
    sketchPad,
    navBar
  }
}
</script>

<style>
#app {
  background: linear-gradient(to top right, #CDDC39 0%, #8BC34A 25%, #FFEB3B 100%);
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  min-width: 600px;
  margin-left: -10px;
  margin-top: -5px;
  margin:-10px;
}
</style>
