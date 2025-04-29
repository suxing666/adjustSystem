<template>
  <div class="info-list">
    <div class="info-header">
      <span class="title">{{ title }}</span>
      <span class="time">{{ currentTime }}</span>
    </div>
    <div class="info-body">
      <div class="info-item" v-for="(item, index) in list" :key="index">
        <span class="label">{{ item.label }}</span>
        <span class="value">{{ item.value }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  title: String,
  list: Array
})

const currentTime = ref('')

function updateTime() {
  const now = new Date()
  const yyyy = now.getFullYear()
  const MM = String(now.getMonth() + 1).padStart(2, '0')
  const dd = String(now.getDate()).padStart(2, '0')
  const hh = String(now.getHours()).padStart(2, '0')
  const mm = String(now.getMinutes()).padStart(2, '0')
  const ss = String(now.getSeconds()).padStart(2, '0')
  currentTime.value = `${yyyy}/${MM}/${dd} ${hh}:${mm}:${ss}`
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

<style scoped>
.info-list {
  background: #001f3f;
  border-radius: 8px;
  padding: 10px;
  color: #00ffff;
  font-size: 14px;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
}

.info-header {
  display: flex;
  justify-content: space-between;
  color: #ffffff;
  font-size: 16px;
  margin-bottom: 10px;
}

.info-body {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}

.info-item {
  display: flex;
  justify-content: space-between;
  padding: 4px 0;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.label {
  color: #00ffff;
}

.value {
  color: #00ffff;
}
</style>
