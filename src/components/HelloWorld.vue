<template>
  <div class="hello">
    <el-button type="primary" @click="test">Hello world!</el-button>
  </div>
</template>

<script>
  import ElButton from '../../node_modules/element-ui/packages/button/src/button'
export default {
    components: {ElButton},
    data () {
      return {
        msg: 'Welcome to Your Vue.js App'
      }
    },
    methods: {
      test () {
        this.$notify({
          title: '提示',
          type: 'success',
          message: '正在导出!'
        })
      }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
