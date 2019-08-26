<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <sketchPad msg="discdisk"/>
  </div>
</template>

<script>
// @ is an alias to /src
import sketchPad from '@/components/sketchPad.vue'

export default {
  name: 'home',
  components: {
    sketchPad
  }
}
</script>
