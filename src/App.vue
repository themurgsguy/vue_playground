<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <hello-world msg="Welcome to Your Vue.js App"/> -->
    <Weather/>
  </div>
</template>

<script>
import Weather from '@/components/Weather.vue'
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    Weather
    // 'hello-world': HelloWorld
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
