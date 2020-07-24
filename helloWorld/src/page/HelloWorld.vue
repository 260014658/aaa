<template>
  <div>
    <el-button type="text" @click="centerDialogVisible = true; getEchartData()">点击打开 Dialog</el-button>
    <el-dialog
      title="图表"
      :visible.sync="centerDialogVisible"
      width="100%">
      <div class="chart" ref="chart"></div>
      <span slot="footer" class="dialog-footer">
        <el-button @click="centerDialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="centerDialogVisible = false">确 定</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      centerDialogVisible: false
    }
  },
  mounted () {
  },
  methods: {
    getEchartData () {
      this.$nextTick(() => {
        const chart = this.$refs.chart
        if (chart) {
          const myChart = this.$echarts.init(chart)
          const option = {
            // 图例，data值要跟series中的name值一致
            legend: {
              data: ['销量']
            },
            title: {
              text: 'ECharts 入门示例'
            },
            xAxis: {
              type: 'category',
              data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
            },
            yAxis: {
              type: 'value'
            },
            // type包括了：line（折线图）、bar（柱状图）、pie（饼图）、scatter（散点图）、graph（关系图）、tree（树图）
            series: [
              {
                name: ['销量'],
                data: [820, 932, 901, 934, 1290, 1330, 1320],
                type: 'bar'
              }
            ]
          }
          myChart.setOption(option)
          window.addEventListener('resize', function () {
            myChart.resize()
          })
        }
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.chart {
  width:600px;
  height:376px;
  margin:0 auto
};

</style>
