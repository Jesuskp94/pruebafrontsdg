<template>
  <CrearTabla/>
</template>

<script>
import CrearTabla from './components/CrearTabla.vue'

export default {
  name: 'App',
  components: {
    CrearTabla
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
.selector-for-some-widget {
  box-sizing: content-box;
}
</style>
