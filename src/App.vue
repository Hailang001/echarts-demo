<template>
  <div id="app">
    <hello-world/>
    <br/>
    <echarts-template></echarts-template>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import EchartsTemplate from './components/EchartsTemplate.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    EchartsTemplate
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
