<template>
  <HelloWorld msg="Hi Lucas" />
  <PolygonDrawer></PolygonDrawer>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import PolygonDrawer from './components/PolygonDrawer.vue';

export default {
  name: 'App',
  components: {
    HelloWorld,
    PolygonDrawer
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
