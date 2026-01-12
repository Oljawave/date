<script setup>
import { ref } from 'vue'
import SplashScreen from './components/SplashScreen.vue'
import DateSteps from './components/DateSteps.vue'
import thinkingImg from './assets/fineas/thinking.png'
import sadImg from './assets/fineas/sad.png'

const showSplash = ref(true)
const showDateSteps = ref(false)
const currentImage = ref(thinkingImg)
const noButtonPosition = ref({ top: 'auto', left: 'auto' })
const noButtonClicked = ref(false)
const mainText = ref('Я хочу воспользоваться методом Адама Сендлера')

const pleadingTexts = [
  'Давай, это будет весело!',
  'Ну соглашайся уже!',
  'Видишь ему грустно'
]

let textIndex = 0

const handleSplashComplete = () => {
  showSplash.value = false
}

const handleYesClick = () => {
  showDateSteps.value = true
}

const moveNoButton = () => {
  const maxX = window.innerWidth - 150
  const maxY = window.innerHeight - 150

  const randomX = Math.floor(Math.random() * maxX)
  const randomY = Math.floor(Math.random() * maxY)

  noButtonPosition.value = {
    top: `${randomY}px`,
    left: `${randomX}px`
  }
}

const handleNoButtonHover = () => {
  if (!noButtonClicked.value) {
    return
  }
  moveNoButton()
}

const handleNoButtonClick = () => {
  currentImage.value = sadImg
  noButtonClicked.value = true

  // Меняем текст на умоляющий
  mainText.value = pleadingTexts[textIndex]
  textIndex = (textIndex + 1) % pleadingTexts.length

  setTimeout(() => {
    moveNoButton()
  }, 100)
}
</script>

<template>
  <SplashScreen v-if="showSplash" @complete="handleSplashComplete" />

  <DateSteps v-else-if="showDateSteps" />

  <div v-else class="main-content">
    <div class="content-wrapper">
      <img :src="currentImage" alt="Character" class="character-image" />
      <h1 class="main-text">{{ mainText }}</h1>
      <button class="action-button action-button-yes" @click="handleYesClick">Ну давай</button>
      <button
        class="action-button action-button-no"
        :class="{ 'shrink': noButtonClicked }"
        :style="{
          top: noButtonPosition.top,
          left: noButtonPosition.left,
          position: noButtonPosition.top !== 'auto' ? 'fixed' : 'static'
        }"
        @click="handleNoButtonClick"
        @mouseenter="handleNoButtonHover"
      >
        Нет
      </button>
    </div>
  </div>
</template>

<style scoped>
.main-content {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
  background: #ffffff;
}

.content-wrapper {
  text-align: center;
  max-width: 500px;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.character-image {
  width: 250px;
  height: auto;
  margin: 0 0 50px 0;
  animation: float 3s ease-in-out infinite;
}

@keyframes float {
  0%, 100% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(-10px);
  }
}

.main-text {
  font-size: 1.2rem;
  color: #333333;
  margin: 0 0 30px 0;
  line-height: 1.5;
  font-weight: 600;
}

.action-button {
  padding: 16px 48px;
  font-size: 1.2rem;
  font-weight: 600;
  border: none;
  border-radius: 50px;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
  margin: 10px;
}

.action-button-yes {
  width: 80%;
  max-width: 300px;
  background: linear-gradient(135deg, #56CCF2 0%, #2F80ED 100%);
  color: #ffffff;
}

.action-button-no {
  width: 80%;
  max-width: 300px;
  background: #ff6b6b;
  color: #ffffff;
  z-index: 10;
  transition: all 0.3s ease;
}

.action-button-no.shrink {
  width: 40%;
  max-width: 150px;
  padding: 12px 24px;
  font-size: 1rem;
}

.action-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
}

.action-button:active {
  transform: translateY(0);
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
}

.action-button-no:hover {
  transform: none;
}

/* Mobile First подход */
@media (min-width: 768px) {
  .character-image {
    width: 320px;
    margin: 0 0 60px 0;
  }

  .main-text {
    font-size: 1.5rem;
    margin: 0 0 40px 0;
  }

  .action-button {
    padding: 18px 60px;
    font-size: 1.3rem;
  }

  .action-button-yes {
    max-width: 350px;
  }

  .action-button-no {
    max-width: 350px;
  }

  .action-button-no.shrink {
    max-width: 180px;
    padding: 14px 28px;
    font-size: 1.1rem;
  }
}

@media (min-width: 1024px) {
  .character-image {
    width: 400px;
    margin: 0 0 70px 0;
  }

  .main-text {
    font-size: 1.8rem;
    margin: 0 0 50px 0;
  }

  .action-button {
    padding: 20px 70px;
    font-size: 1.5rem;
  }

  .action-button-yes {
    max-width: 400px;
  }

  .action-button-no {
    max-width: 400px;
  }

  .action-button-no.shrink {
    max-width: 200px;
    padding: 16px 32px;
    font-size: 1.2rem;
  }
}
</style>
