<template>
  <div class="container">
    <div class="ip-box">
     访问IP  {{ ip }}
    </div>
    <div class="poster-box">

      <img src="@/assets/0d75fc42b6987.avif" alt="isLxhimg">
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
.container {
  display: flex;
  flex-direction: column;
  height: 100vh;
  background-color: #1e1e1e;
  color: white;
  align-items: center;
  justify-content: flex-start;
}

.ip-box {
  width: 100%;
  text-align: center;
  padding: 20px 0;
  font-size: 24px;
  background-color: #000;
  border-bottom: 2px solid #444;
}

.poster-box {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
}

.poster-img {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
  border: 1px solid #333;
  background-color: #000;
}
</style>
