<template>
  <div class="hello">
    <el-button type="primary" @click="test"><span v-if="show">显示</span><span v-if="!show">隐藏</span></el-button>
  </div>
</template>

<script>
  import ElButton from '../../node_modules/element-ui/packages/button/src/button'
export default {
    components: {ElButton},
    data () {
      return {
        show: false
      }
    },
    methods: {
      test () {
        this.show = !this.show
        this.$emit('send', this.show)
        if (this.show === false) {
          this.$notify({
            title: '提示',
            type: 'success',
            message: '已显示!'
          })
        } else {
          this.$notify({
            title: '提示',
            type: 'warning',
            message: '已隐藏!'
          })
        }
      }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
