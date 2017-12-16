<template>
  <div id="app">
    <hello-world @send="send"></hello-world>
    <br/>
    <echarts-template v-if="chartShow"></echarts-template>
    <br />
    <echarts-tem></echarts-tem>
    <br />
    <charts></charts>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import EchartsTemplate from './components/EchartsTemplate.vue'
import EchartsTem from './components/EchartsTem.vue'
import Charts from './components/Charts.vue'

export default {
  name: 'app',
  data () {
    return {
      chartShow: true
    }
  },
  methods: {
    send (data) {
      this.chartShow = !data
      // console.log(data)
    }
  },
  mounted () {
  },
  components: {
    HelloWorld,
    EchartsTemplate,
    EchartsTem,
    Charts
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
