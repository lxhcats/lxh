<template>
  <div class="container">
    <div class="ip-box">
     访问IP  {{ ip }}
    </div>
    <div class="poster-box">

      <img src="@/assets/110000.avif" alt="isLxhimg">
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import axios from 'axios'

const ip = ref('加载中...')

onMounted(async () => {
  try {
    const response = await axios.get('https://api.lxhcat.net/ip')
    ip.value = response.data.ip || '未知 IP'
  } catch (error) {
    ip.value = '获取失败'
    console.error(error)
  }
})
</script>

<style scoped>
..container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  background-color: #1e1e1e;
  color: white;
  align-items: center;
  justify-content: flex-start;
  padding: 0;
  margin: 0;
}

/* IP展示区域 */
.ip-box {
  width: 100%;
  text-align: center;
  padding: 16px;
  font-size: 1.5rem;
  background-color: #000;
  border-bottom: 2px solid #444;
  box-sizing: border-box;
}

/* 图片展示区域 */
.poster-box {
  flex: 1;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 16px;
  box-sizing: border-box;
}

.poster-img {
  width: 100%;
  max-width: 400px;
  height: auto;
  border: 1px solid #333;
  background-color: #000;
  border-radius: 8px;
}

/* 响应式布局 */
@media (max-width: 600px) {
  .ip-box {
    font-size: 1.2rem;
    padding: 12px;
  }

  .poster-box {
    padding: 12px;
  }

  .poster-img {
    max-width: 90vw;
    border-radius: 6px;
  }
}
</style>
