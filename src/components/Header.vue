<template>
  <div class="header">
    <h2 class="title">公用事业部智能调度系统</h2>
    <span class="time">{{ currentTime }}</span>
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
  updateTime()
  timer = setInterval(updateTime, 1000)
})

onUnmounted(() => {
  clearInterval(timer)
})
</script>

<script>
export default {
  name: 'Header',
}
</script>

<style scoped>
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
</style>
