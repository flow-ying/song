<template>
  <div class="app">
    <!-- 图片容器 -->
    <div class="image-container">
      <img 
        :src="currentImage" 
        :alt="getImageName(currentIndex)"
        class="fullscreen-image"
      />
    </div>

    <!-- 左箭头 -->
    <button 
      v-if="currentIndex > 0"
      class="arrow arrow-left" 
      @click="prevImage"
    >
      ←
    </button>

    <!-- 右箭头 -->
    <button 
      v-if="currentIndex < images.length - 1"
      class="arrow arrow-right" 
      @click="nextImage"
    >
      →
    </button>

    <!-- 图片指示器（可选） -->
    <div class="indicator">
      {{ currentIndex + 1 }} / {{ images.length }}
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

// 图片列表（按顺序）
const images = [
  '/photos/start.png',
  '/photos/1zhicha.png',
  '/photos/2suicha.png',
  '/photos/3niancha.png',
  '/photos/4mocha.png',
  '/photos/5luocha.png',
  '/photos/6houtang.png',
  '/photos/7tangzhan.png',
  '/photos/8diancha.png',
  '/photos/end.png'
]

const currentIndex = ref(0)

// 当前图片
const currentImage = ref(images[0])

// 获取图片名称（用于alt属性）
const getImageName = (index) => {
  const names = [
    '开始',
    '炙茶',
    '碎茶',
    '碾茶',
    '磨茶',
    '罗茶',
    '候汤',
    '汤盏',
    '点茶',
    '结束'
  ]
  return names[index] || `图片${index + 1}`
}

// 上一张
const prevImage = () => {
  if (currentIndex.value > 0) {
    currentIndex.value--
    currentImage.value = images[currentIndex.value]
  }
}

// 下一张
const nextImage = () => {
  if (currentIndex.value < images.length - 1) {
    currentIndex.value++
    currentImage.value = images[currentIndex.value]
  }
}

// 键盘支持
const handleKeyPress = (e) => {
  if (e.key === 'ArrowLeft') {
    prevImage()
  } else if (e.key === 'ArrowRight') {
    nextImage()
  }
}

// 监听键盘事件
onMounted(() => {
  window.addEventListener('keydown', handleKeyPress)
})

onUnmounted(() => {
  window.removeEventListener('keydown', handleKeyPress)
})
</script>

<style scoped>
.app {
  width: 100vw;
  height: 100vh;
  position: relative;
  overflow: hidden;
  background: #000;
}

.image-container {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  position: relative;
  padding: 0;
}

.fullscreen-image {
  width: 100vw;
  height: 100vh;
  object-fit: cover;
  object-position: left center;
  user-select: none;
  -webkit-user-select: none;
  display: block;
}

/* 箭头按钮 */
.arrow {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  width: 60px;
  height: 60px;
  background: rgba(0, 0, 0, 0.6);
  border: none;
  color: white;
  font-size: 32px;
  font-weight: bold;
  cursor: pointer;
  z-index: 100;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  transition: all 0.2s ease;
  user-select: none;
  -webkit-tap-highlight-color: transparent;
}

.arrow:active {
  background: rgba(0, 0, 0, 0.8);
  transform: translateY(-50%) scale(0.9);
}

.arrow-left {
  left: 15px;
}

.arrow-right {
  right: 15px;
}

/* 指示器 */
.indicator {
  position: absolute;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
  background: rgba(0, 0, 0, 0.6);
  color: white;
  padding: 8px 16px;
  border-radius: 20px;
  font-size: 14px;
  z-index: 100;
}

/* 手机端适配 */
@media (max-width: 768px) {
  .arrow {
    width: 50px;
    height: 50px;
    font-size: 28px;
  }

  .arrow-left {
    left: 10px;
  }

  .arrow-right {
    right: 10px;
  }

  .indicator {
    font-size: 12px;
    padding: 6px 12px;
    bottom: 15px;
  }
}

/* 所有图片统一从左边对齐，超出部分裁切 */
@media (orientation: landscape) {
  .fullscreen-image {
    width: 100vw;
    height: 100vh;
    object-fit: cover;
    object-position: left center;
  }
}

@media (orientation: portrait) {
  .fullscreen-image {
    width: 100vw;
    height: 100vh;
    object-fit: cover;
    object-position: left center;
  }
}
</style>

