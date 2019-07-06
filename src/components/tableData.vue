<template>
  <div class="hello">
    <div class="select-group">
      <el-radio-group
        v-model="selsectedK"
        @change="requestData"
      >
        <el-radio-button label="一分钟"></el-radio-button>
        <el-radio-button label="三分钟"></el-radio-button>
        <el-radio-button label="五分钟"></el-radio-button>
        <el-radio-button label="十五分钟"></el-radio-button>
      </el-radio-group>
    </div>
    <el-table
      :data="tableData"
      border
      v-loading="loading"
     >
      <el-table-column
        v-for="item in tableHeader"
        :key="item.title"
        :prop="item.field"
        :label="item.title"
        align="center"
      >
        <template
          v-if="item.title !== '策略'"
          slot="header"
        >
          {{ item.title }}
          <br />
          <el-tag type="danger">{{ item.scale1 }}</el-tag> : <el-tag type="success">{{ item.scale2 }}</el-tag>
        </template>
        <template slot-scope="scope">
          <span
            v-if="item.title === '策略'"
          >
            <el-button type="text"> {{ scope.row[item.field] }} </el-button>
          </span>
          <span
            v-else
          >
            <el-button
              type="text"
              @click="open"
              :style="scope.row[item.field] === '空头持仓' ? 'color: #67C23A' : scope.row[item.field] === '多头平仓' ? 'color: #F56C6C' : 'color: #909399' "
            >
              {{ scope.row[item.field] }}
            </el-button>
          </span>
        </template>
      </el-table-column>
    </el-table>
    <chart
      :openChart="openChart"
      @closeChart="closeChart"
    />
  </div>
</template>

<script>
import mockTableData from '../assets/mock-table-data.json';
import chart from './chart.vue'
export default {
  name: 'HelloWorld',
  components: {
    chart,
  },
  data () {
    return {
      tableData: mockTableData.data,
      openChart: false,
      loading: false,
      selsectedK: '十五分钟',
      tableHeader: [
        {
          title: '策略',
          field: 'tactics',
        },
        {
          title: '螺旋主力',
          field: 'spiralForce',
          scale1: 1,
          scale2: 2,
        },
        {
          title: '铁矿主力',
          field: 'ironForce',
          scale1: 3,
          scale2: 2,
        },
        {
          title: '豆粕主力',
          field: 'beeForce',
          scale1: 1,
          scale2: 3,
        },
        {
          title: 'PTA主力',
          field: 'PTAForce',
          scale1: 3,
          scale2: 2,
        },
        {
          title: '菜粕主力',
          field: 'greensFroce',
          scale1: 4,
          scale2: 3,
        },
      ]
    }
  },
  mounted () {
    this.requestData();
    this.updateData();
  },
  methods: {
    requestData () {
      this.loading = true;
      const _this = this;
      setTimeout(()=>{
        this.loading = false;
      } , 500);
    },
    updateData () {
      setInterval(() => {
        this.requestData();
      }, 1000 * 60);
    },
    open () {
      console.log(this.openChart, '--------------')
      this.openChart = true;
    },
    closeChart () {
      this.openChart = false;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.select-group {
  margin-bottom: 20px;
}
</style>
