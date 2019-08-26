<template>
  <div id="app" >
    <navBar/>
     <router-view></router-view>
  </div>
</template>



<script>
import navBar from './components/navBar'
export default {
  name: 'app',
  components: {
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
  min-height: 800px;
  margin-left: -10px;
  /* margin-top: -5px; */
  margin:-10px;
}
</style>
