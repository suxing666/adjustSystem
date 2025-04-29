<template>
  <div class="app-container">
    <!-- 顶部导航栏 -->
    <div class="header">
      <h2 class="title">公用事业部智能调度系统</h2>
      <span class="time">{{ currentTime }}</span>
    </div>

    <!-- 三栅＋底部两块 都在同一个 grid-container 里 -->
    <div class="main-content">
      <div class="grid-container">
        <!-- 第一行 第1栅：实时电负荷和实时热负荷 -->
        <div class="left-grid">
          <div class="chart"><h3>实时电负荷</h3></div>
          <div class="chart"><h3>实时热负荷</h3></div>
        </div>

        <!-- 第一行 第2栅：机组实施信息显示 -->
        <div class="middle-grid">
          <h3>机组实施信息显示</h3>
        </div>

        <!-- 第一行 第3栅：实时成本和其他信息 -->
        <div class="right-grid">
          <div class="chart"><h3>实时成本</h3></div>
          <div class="chart"><h3>其他信息</h3></div>
        </div>

        <!-- 第二行 第1、2栅合并：负荷调整 -->
        <div class="load-adjust">
          <h3>负荷调整</h3>
        </div>

        <!-- 第二行 第3栅：预警信息 -->
        <div class="alert-info">
          <h3>预警信息</h3>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const currentTime = ref('')

// 更新时间函数
function updateTime() {
  currentTime.value = new Date().toLocaleString()
}

let timer
onMounted(() => {
  updateTime()              // 立刻获取一次
  timer = setInterval(updateTime, 1000)  // 每秒更新一次
})

onUnmounted(() => {
  clearInterval(timer)
})

</script>

<script>
export default {
  name: "App",
};
</script>

<style scoped>
.app-container {
  display: flex;
  flex-direction: column;
  padding: 20px;
}

.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: #003366;
  padding: 10px;
  height: 60px;
}

.title {
  flex: 1;
  margin: 0;
  text-align: center;
  color: white;
  font-size: 24px;
}

.time {
  color: white;
  margin-right: 5px;
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

/* 第一行第1栅：上下两块 */
.left-grid,
.right-grid {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

/* 第一行第2栅：机组实施信息显示 */
.middle-grid {
  background: #f4f4f4;
  border-radius: 8px;
  padding: 5px;   
}

/* chart 样式共用 */
.chart {
  height: 200px;
  background: #f4f4f4;
  border-radius: 8px;
  display: flex;
  justify-content: flex-start;
  align-items: flex-start;
  padding: 5px;  
}

/* 标题样式 */
.chart h3 {
  margin: 5px;
  text-align: left;
}

/* 第二行 “负荷调整” 横跨前两列 */
.load-adjust {
  grid-column: 1 / span 2;
  background: #f4f4f4;
  border-radius: 8px;
  padding: 15px;
}

/* 第二行 “预警信息” 在第3列 */
.alert-info {
  grid-column: 3;
  background: #f4f4f4;
  border-radius: 8px;
  padding: 15px;
}
</style>
