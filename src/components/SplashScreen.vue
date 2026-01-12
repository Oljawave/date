<template>
  <div class="splash-screen" :class="{ 'fade-out': fadeOut }">
    <div class="splash-content">
      <img
        src="../assets/Duplo.png"
        alt="Duplo"
        class="splash-image"
        :class="{ 'animate': animateImage }"
      />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const animateImage = ref(false)
const fadeOut = ref(false)

const emit = defineEmits(['complete'])

onMounted(() => {
  // Запуск анимации появления и увеличения
  setTimeout(() => {
    animateImage.value = true
  }, 100)

  // Начало fade out через 3 секунды
  setTimeout(() => {
    fadeOut.value = true
  }, 3000)

  // Завершение splash screen через 3.5 секунды
  setTimeout(() => {
    emit('complete')
  }, 3500)
})
</script>

<style scoped>
.splash-screen {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background: linear-gradient(135deg, #56CCF2 0%, #2F80ED 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 9999;
  transition: opacity 0.5s ease-out;
  opacity: 1;
}

.splash-screen.fade-out {
  opacity: 0;
}

.splash-content {
  text-align: center;
}

.splash-image {
  width: 150px;
  height: auto;
  opacity: 0;
  transform: scale(0.3);
  transition: all 1s cubic-bezier(0.34, 1.56, 0.64, 1);
}

.splash-image.animate {
  opacity: 1;
  transform: scale(1);
}

/* Mobile First - базовые стили для мобильных */
@media (min-width: 375px) {
  .splash-image {
    width: 180px;
  }
}

@media (min-width: 768px) {
  .splash-image {
    width: 250px;
  }
}

@media (min-width: 1024px) {
  .splash-image {
    width: 300px;
  }
}
</style>
