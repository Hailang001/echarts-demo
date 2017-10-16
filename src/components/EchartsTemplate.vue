<template>
  <div>
    <div id="draw"></div>
    <div id="draw2"></div>
    <div id="draw3"></div>
  </div>
</template>
<script type="text/ecmascript-6">
  import echarts from 'echarts'
  export default {
    data () {
      return {
        color: [
          ['rgba(224,4,52, 0.3)', 'rgba(224,4,52, 0)', 'rgb(224,4,52)', 'rgba(224,4,52,0.27)'],
          ['rgba(27, 107, 155, 0.3)', 'rgba(27, 107, 155, 0)', 'rgb(27, 107, 155)', 'rgba(27, 107, 155,0.27)'],
          ['rgba(36, 144, 66, 0.3)', 'rgba(36, 144, 66, 0)', 'rgb(36, 144, 66)', 'rgba(36, 144, 66,0.27)'],
          ['rgba(239, 179, 4, 0.3)', 'rgba(239, 179, 4, 0)', 'rgb(239, 179, 4)', 'rgba(239, 179, 4,0.27)'],
          ['rgba(147, 67, 131, 0.3)', 'rgba(147, 67, 131, 0)', 'rgb(147, 67, 131)', 'rgba(147, 67, 131,0.27)'],
          ['rgba(266, 112, 60, 0.3)', 'rgba(266, 112, 60, 0)', 'rgb(266, 112, 60)', 'rgba(266, 112, 60,0.27)'],
          ['rgba(101, 188, 232, 0.3)', 'rgba(101, 188, 232, 0)', 'rgb(101, 188, 232)', 'rgba(101, 188, 232,0.27)'],
          ['rgba(224, 101, 152, 0.3)', 'rgba(224, 101, 152, 0)', 'rgb(224, 101, 152)', 'rgba(224, 101, 152,0.27)'],
          ['rgba(117, 160, 154, 0.3)', 'rgba(117, 160, 154, 0)', 'rgb(117, 160, 154)', 'rgba(117, 160, 154,0.27)']
        ],
        value: [
          [20, 30, 40, 50, 10, 70, 60],
          [40, 20, 10, 60, 30, 10, 50],
          [70, 40, 50, 20, 50, 80, 20],
          [40, 60, 60, 10, 60, 90, 70],
          [50, 10, 70, 80, 70, 20, 10],
          [10, 30, 50, 30, 10, 30, 10],
          [30, 20, 30, 20, 40, 30, 50],
          [60, 50, 60, 50, 60, 50, 60],
          [70, 50, 70, 50, 70, 60, 80]
        ],
        nameList: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I'],
        series: [],
        legend: []
      }
    },
    methods: {
      getLegend () {
        let selected = []
        for (let i = 0, ii = this.nameList.length; i < ii; i++) {
          var temp = `this.nameList[i]:true`
          selected = selected.concat(temp)
        }
        var legend = {
          icon: 'rect',
          itemWidth: 14,
          itemHeight: 5,
          itemGap: 13,
          data: this.nameList,
          selected: selected,
          right: '4%',
          bottom: '2%',
          textStyle: {
            fontSize: 12,
            color: '#62c0e0'
          }
        }
        this.legend = legend
      },
      getSeries () {
        let series = []
        for (let i = 0, ii = this.value.length; i < ii; i++) {
          let temp = [{
            name: this.nameList[i],
            type: 'line',
            smooth: true, //  平滑曲线
            symbol: 'circle', //  鼠标标记图形
            symbolSize: 5, //  鼠标标记图形大小
            showSymbol: false, //  显示标记点
            lineStyle: {
              normal: {
                width: 1
              }
            },
            areaStyle: { //  面积
              normal: {
                color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                  offset: 0,
                  color: this.color[i][0]
                }, {
                  offset: 0.8,
                  color: this.color[i][1]
                }], false),
                shadowColor: 'rgba(0, 0, 0, 0.1)',
                shadowBlur: 10
              }
            },
            itemStyle: { //  折线的拐点样式
              normal: {
                color: this.color[i][2],
                borderColor: this.color[i][3],
                borderWidth: 12
              }
            },
            data: this.value[i]
          }]
          series = series.concat(temp)
        }
        this.series = series
      },
      drawGraph () {
        var myChart = echarts.init(document.getElementById('draw'))
        var myChart2 = echarts.init(document.getElementById('draw2'))
        window.onresize = function () {
          myChart.resize()
          myChart2.resize()
        }
       // window.onresize = myChart.resize
        myChart.showLoading()
        //  set
        try {
          myChart.setOption({
            //  option的配置开始
            title: { //  标题
              text: '这是标题',
              padding: [15, 5],
              x: 'center',
              textStyle: {
                fontWeight: 600,
                fontSize: 16,
                color: '#0f0f0f'
              }
            },
            tooltip: { //  提示
              trigger: 'axis',
              axisPointer: {
                lineStyle: {
                  color: '#57617B'
                }
              },
              textStyle: {
                fontWeight: 200,
                fontSize: 8,
                color: '#fff'
              }
            },
            legend: this.legend,
            grid: { //  绘制位置
              left: '10%',
              right: '15%',
              bottom: '20%',
              containLabel: true
            },
            xAxis: [{ //  X轴
              type: 'category',
              boundaryGap: false,
              axisLine: { //  轴线
                lineStyle: {
                  color: '#75a09a'
                }
              },
              data: ['星期一', '星期二', '星期三', '星期四', '星期五', '星期六', '星期日']
            }],
            yAxis: [{ //  Y轴
              type: 'value',
              name: '%',
              axisTick: {
                show: false
              },
              axisLine: {  //  轴线
                lineStyle: {
                  color: '#75a09a'
                }
              },
              axisLabel: { //  文字距离Y轴
                margin: 10,
                textStyle: {
                  fontSize: 14
                }
              },
              splitLine: { //  栅格线
                lineStyle: {
                  color: '#e9e8e8'
                }
              }
            }],
            //  系列配置
            series: this.series
            // 以上为option的配置结束
          })
        } catch (e) {
          console.log(e + '报错啦')
        }
        try {
          myChart2.setOption({
            //  option的配置开始
            title: { //  标题
              text: '这是标题',
              padding: [15, 5],
              x: 'center',
              textStyle: {
                fontWeight: 600,
                fontSize: 16,
                color: '#0f0f0f'
              }
            },
            tooltip: { //  提示
              trigger: 'axis',
              axisPointer: {
                lineStyle: {
                  color: '#57617B'
                }
              },
              textStyle: {
                fontWeight: 200,
                fontSize: 8,
                color: '#fff'
              }
            },
            legend: this.legend,
            grid: { //  绘制位置
              left: '10%',
              right: '15%',
              bottom: '20%',
              containLabel: true
            },
            xAxis: [{ //  X轴
              type: 'category',
              boundaryGap: false,
              axisLine: { //  轴线
                lineStyle: {
                  color: '#75a09a'
                }
              },
              data: ['星期一', '星期二', '星期三', '星期四', '星期五', '星期六', '星期日']
            }],
            yAxis: [{ //  Y轴
              type: 'value',
              name: '%',
              axisTick: {
                show: false
              },
              axisLine: {  //  轴线
                lineStyle: {
                  color: '#75a09a'
                }
              },
              axisLabel: { //  文字距离Y轴
                margin: 10,
                textStyle: {
                  fontSize: 14
                }
              },
              splitLine: { //  栅格线
                lineStyle: {
                  color: '#e9e8e8'
                }
              }
            }],
            //  系列配置
            series: this.series
            // 以上为option的配置结束
          })
        } catch (e) {
          console.log(e + '报错啦')
        }
        myChart.hideLoading()
      }
    },
    mounted () {
      this.getSeries()
      this.getLegend()
      this.drawGraph()
    }
  }
</script>
<style scoped>
  #draw{
    width: 46%;
    height:300px;
    margin: 0 auto;
    border: solid 1px gray;
    float: left;
  }
  #draw2{
    width: 46%;
    height:300px;
    margin: 0 auto;
    border: solid 1px gray;
    float: right;
  }
</style>
