<template>
  <div id="app">
    <Videos/>
  </div>
</template>

<script>

import Videos from './components/Videos'

export default {
  name: 'App',
  components: {
    Videos
  }
}
</script>

<style>
body{
  background: #292929;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
