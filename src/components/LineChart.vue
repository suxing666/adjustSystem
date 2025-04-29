<template>
  <div class="line-chart-container">
    <div class="chart-title">{{ title }}</div>
    <div ref="chartRef" class="chart-content"></div>
  </div>
</template>

<script setup>
import * as echarts from 'echarts'
import { onMounted, ref, watch } from 'vue'

const props = defineProps({
  title: String,
  data: Array
})

const chartRef = ref(null)

onMounted(() => {
  const myChart = echarts.init(chartRef.value)
  const option = {
    grid: {
        top: 10,
        left: '10%',
        right: '10%',
        bottom: '15%'
    },
    xAxis: {
        type: 'value',
        min: 0,
        max: 7,
        splitNumber: 7,
        axisLine: { show: true, lineStyle: { color: '#ffffff' } }, // 显示 x 轴轴线
        axisTick: { show: false }, // 不显示刻度线
        axisLabel: {
            show: true,
            color: '#ffffff',
            formatter: function (value) {
            // 如果是0，不显示
            return value === 0 ? '' : value
            }
        },
        splitLine: {
            show: true,
            lineStyle: {
            type: 'dashed',
            color: '#666'
            }
        }
    },
    yAxis: {
        type: 'value',
        min: 0,
        axisLine: { show: false },     // 隐藏 y 轴轴线
        axisTick: { show: false },     // 隐藏 y 轴刻度线
        axisLabel: { show: true, color: '#ffffff' },  // 显示 y 轴数字
        splitLine: {
            show: true,
            lineStyle: {
            type: 'dashed',
            color: '#666'
            }
        }
    },
    series: [
      {
        data: props.data,
        type: 'line',
        smooth: false,
        symbol: 'circle',
        itemStyle: {
          color: '#FFD700'
        },
        lineStyle: {
          color: '#FFD700'
        },
        areaStyle: {
          color: 'rgba(255, 215, 0, 0.2)'
        }
      }
    ],
    backgroundColor: '#001f3f'
  }

  myChart.setOption(option)
})
</script>

<style scoped>
.line-chart-container {
  background: #001f3f;
  border-radius: 8px;
  padding: 10px;
  display: flex;
  flex-direction: column;
}

.chart-title {
  font-size: 16px;
  color: #ffffff;
  margin-bottom: 8px;
  text-align: left;
}

.chart-content {
  width: 100%;
  height: 180px;
}
</style>
