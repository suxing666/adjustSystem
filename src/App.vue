<script setup>
// 引入各个子组件
import Header from './components/Header.vue'
import LineChart from './components/LineChart.vue'
import InfoList from './components/InfoList.vue'
import LoadAdjust from './components/LoadAdjust.vue'
import AlertInfo from './components/AlertInfo.vue'

const 电负荷数据 = [
  [1, 1],
  [2, 4],
  [3, 2],
  [4, 3],
  [5, 3],
  [6, 2],
  [7, 3]
]

const 热负荷数据 = [
  [1, 2],
  [2, 3],
  [3, 1],
  [4, 4],
  [5, 2],
  [6, 3],
  [7, 2]
]

const 成本数据 = [
  [1, 3],
  [2, 2],
  [3, 2],
  [4, 2],
  [5, 3],
  [6, 4],
  [7, 3]
]
</script>

<template>
  <div class="app-container">
    <!-- 顶部导航栏 -->
    <Header />

    <!-- 主体内容 -->
    <div class="main-content">
      <div class="grid-container">
        <!-- 第一行 第1栅：实时电负荷 和 实时热负荷 -->
        <div class="left-grid">
          <LineChart title="实时电负荷" :data="电负荷数据" />
          <LineChart title="实时热负荷" :data="热负荷数据" />
        </div>

        <!-- 第一行 第2栅：机组实施信息显示 -->
        <div class="middle-grid">
          <h3>机组实施信息显示</h3>
        </div>

        <!-- 第一行 第3栅：实时成本 和 其他信息 -->
        <div class="right-grid">
           <LineChart title="实时成本" :data="成本数据" />
          <InfoList
            title="其他信息"
            :list="[
              { label: '实时电价:', value: '00000' },
              { label: '实时燃料价格:', value: '00000' },
              { label: '昨日发电量:', value: '00000' },
              { label: '昨日购电量:', value: '00000' }
            ]"
          />
        </div>

        <!-- 第二行 第1-2栅合并：负荷调整 -->
        <LoadAdjust />

        <!-- 第二行 第3栅：预警信息 -->
        <AlertInfo />
      </div>
    </div>
  </div>
</template>

<style scoped>
.app-container {
  display: flex;
  flex-direction: column;
  padding: 20px;
}

.main-content {
  margin-top: 20px;
}

.grid-container {
  display: grid;
  grid-template-columns: 34.5% 34.5% 29%;
  grid-auto-rows: auto;
  gap: 20px;
}

/* 第一行第1栅、第三栅上下两块 */
.left-grid,
.right-grid {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

/* 第一行第2栅：机组实施信息 */
.middle-grid {
  background: #f4f4f4;
  border-radius: 8px;
  padding: 5px;
}

/* 第二行第1、2栅合并 */
.load-adjust {
  grid-column: 1 / span 2;
  background: #f4f4f4;
  border-radius: 8px;
  padding: 15px;
}

/* 第二行第3栅 */
.alert-info {
  grid-column: 3;
  background: #f4f4f4;
  border-radius: 8px;
  padding: 15px;
}

/* 响应式布局，适配小屏幕 */
@media (max-width: 768px) {
  .grid-container {
    grid-template-columns: 1fr;
  }

  .load-adjust, .alert-info {
    grid-column: 1;
  }

  .left-grid, .right-grid {
    gap: 10px;
  }
}

@media (max-width: 480px) {
  .app-container {
    padding: 10px;
  }

  .grid-container {
    gap: 10px;
  }

  .middle-grid,
  .load-adjust,
  .alert-info {
    padding: 10px;
  }
}
</style>
