<template>
  <el-dialog :visible.sync="v">
      <div class="chart">

      </div>
  </el-dialog>
</template>

<script>
import echarts from 'echarts'
import option from './chartOption'
export default {
  props: {
    openChart: {
      type: Boolean,
      default: false,
    },
  },
  data () {
    return {
      v: false,
    }
  },
  watch: {
    openChart (val) {
      this.v = val;
      if (val) {
        this.$nextTick(() => {
          const dom = this.$el.querySelector('.chart');
          const chart = echarts.init(dom);
          chart.setOption(option);
        })
      }
    },
    v (val) {
      if (!val) {
        this.$emit('closeChart', val);
      }
    }
  },
  mounted () {
    // console.log(option);
  }
}
</script>


<style>
.chart {
  height: 500px;
  background-color: bisque;
}
</style>

