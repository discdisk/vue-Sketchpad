<template>
<div>
    
    <nav>
      <router-link to="/">SketchPad</router-link>
      <router-link to="/about">About</router-link>
      <a href="https://discdisk.github.io/sketchpad-deploy">github page</a>
    </nav>
    <div style="padding:25px"></div>

</div>

</template>

<script>
export default {
  name: 'navBar'
}
</script>

<style scoped>
nav{
    /* display: -webkit-flex;
    display: flex; */
    position: fixed;
    width: 100%;
    
    background-color: #333;
    overflow: hidden;
    padding-right: 5px;
}
nav a{
    
    /* flex:1;
    -webkit-box-flex: 1; */

    float: right;
    color: #f2f2f2;
    text-align: center;
    padding: 14px 16px;
    text-decoration: none;
    font-size: 17px;
}
nav a:hover {
  background-color: #ddd;
  color: black;
}
nav a:active {
  background-color: #4CAF50;
  color: white;
}
</style>
