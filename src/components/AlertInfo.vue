<template>
  <div class="alert-box">
    <div class="alert-header">
      <span class="alert-icon">▶</span>
      <span class="alert-title">预警信息</span>
    </div>

    <div class="alert-content">
      <!-- 异常点 -->
      <div class="row">
        <span class="label gradient-text">异常点</span>
        <div class="value gradient-box">异常点异常点异常点</div>
      </div>

      <!-- 异常原因 -->
      <div class="row">
        <span class="label gradient-text">异常原因</span>
        <div class="value gradient-box multiline">
          异常原因异常原因异常原因异常原因异常原因<br />
          异常原因异常原因异常原因
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
// 暂无 props，如需动态内容可扩展
</script>

<style scoped>
/* 整体盒子 */
.alert-box {
  background: #001f3f;
  border: 2px solid #ff6600;
  border-radius: 8px;
  padding: 10px 15px;
  color: #ffffff;
  font-family: 'Microsoft YaHei', sans-serif;
  display: flex;
  flex-direction: column;
  height: 100%;
}

/* 标题部分 */
.alert-header {
  display: flex;
  align-items: center;
  font-size: 18px;
  font-weight: bold;
  margin-bottom: 10px;
  color: #ffffff;
}

.alert-icon {
  color: #ffcc00;
  margin-right: 6px;
}

.alert-title {
  color: #ffffff;
}

/* 内容主体 */
.alert-content {
  display: flex;
  flex-direction: column;
  gap: 10px;
  font-size: 14px;
}

/* 每一行：异常点、异常原因 */
.row {
  display: flex;
  align-items: flex-start;
  gap: 10px;
}

.label {
  width: 70px;
  font-weight: bold;
}

/* 渐变字体：白到红 */
.gradient-text {
  background: linear-gradient(to right, #ffffff,rgb(195, 90, 90));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

/* 内容显示区域 */
.gradient-box {
  flex: 1;
  position: relative;
  background: #001f3f; /* 背景和整体统一 */
  color: #ffffff;
  padding: 12px 10px;
  border-radius: 4px;
  overflow: hidden;
}

/* 上边渐变线 */
.gradient-box::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  height: 2px;
  width: 100%;
  background: linear-gradient(to right, transparent, #ff4444, transparent);
}

/* 下边渐变线 */
.gradient-box::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  height: 2px;
  width: 100%;
  background: linear-gradient(to right, transparent, #ff4444, transparent);
}

/* 多行文字处理 */
.multiline {
  white-space: normal;
  line-height: 1.6;
}
</style>
