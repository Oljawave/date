<template>
  <div class="date-steps">
    <!-- Счастливая картинка -->
    <div v-if="currentStep === 0" class="step-content fade-in-out">
      <img src="../assets/fineas/happy.png" alt="Happy" class="happy-image" />
    </div>

    <!-- Заголовок программы -->
    <div v-if="currentStep === 1" class="step-content fade-in-out">
      <h1 class="program-title">Итак трехступенчатая программа Адама Сендлера</h1>
    </div>

    <!-- Шаг #1 -->
    <div v-if="currentStep === 2" class="step-content fade-in-out">
      <h2 class="step-title">Шаг #1</h2>
    </div>

    <!-- Первый анекдот -->
    <div v-if="currentStep === 3" class="step-content fade-in-out">
      <div class="joke-simple">
        <p class="joke-line">Едут два армянина инвалида по пустыне.</p>
        <p class="joke-line">Вдруг видят лампу, потерли ее и вылез Джин.</p>
        <p class="joke-line">Джин им говорит:</p>
        <p class="joke-line highlight">"Я исполню одно любое ваше желание. Но так как вас двое, то желание будет пополам на двоих работать."</p>
        <p class="joke-line">Армяне посовещались и говорят Джину:</p>
        <p class="joke-line highlight">"Мы хотим снова ходить."</p>
        <p class="joke-line">"Хорошо. Но так как желание надо разделить, то ходить вы будете по очереди."</p>
        <p class="joke-punchline">И дал им нарды</p>
      </div>
    </div>

    <!-- Ну ладно согласен другую -->
    <div v-if="currentStep === 4" class="step-content fade-in-out">
      <p class="transition-text">Ну ладно согласен другую</p>
    </div>

    <!-- Второй анекдот -->
    <div v-if="currentStep === 5" class="step-content fade-in-out">
      <p class="joke-simple-text">Чернокожий человек рассказал анекдот, но его никто не выкупил</p>
    </div>

    <!-- Hard картинка -->
    <div v-if="currentStep === 6" class="step-content fade-in-out">
      <img src="../assets/fineas/hard.png" alt="Hard" class="reaction-image" />
      <p class="hope-text">Надеюсь хотя бы улыбнулась потому что...</p>
    </div>

    <!-- Compliment -->
    <div v-if="currentStep === 7" class="step-content fade-in-out">
      <img src="../assets/fineas/compliment.png" alt="Compliment" class="compliment-image" />
      <h2 class="compliment-text">✨У тебя очень красивая улыбка✨</h2>
    </div>

    <!-- Final invitation -->
    <div v-if="currentStep === 8" class="step-content fade-in-out">
      <img src="../assets/fineas/flowers.png" alt="Flowers" class="flowers-image" />
      <h2 class="invitation-text">Пойдем на свидание?</h2>
      <div class="final-buttons">
        <button class="action-button action-button-yes">Давай, обсудим детали</button>
        <button class="action-button action-button-no" disabled>Нет</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const currentStep = ref(0)

const stepDurations = [
  2000,  // Счастливая картинка - 2 сек
  3000,  // Заголовок программы - 3 сек
  2000,  // Шаг #1 - 2 сек
  25000, // Первый анекдот - 25 сек (увеличено время на чтение)
  2500,  // Ну ладно согласен - 2.5 сек
  5000,  // Второй анекдот - 5 сек
  3500,  // Hard картинка с текстом - 3.5 сек
  4000,  // Compliment - 4 сек
  Infinity,  // Final invitation - остается навсегда
]

onMounted(() => {
  let totalDelay = 0

  stepDurations.forEach((duration, index) => {
    setTimeout(() => {
      currentStep.value = index
    }, totalDelay)
    totalDelay += duration
  })
})
</script>

<style scoped>
.date-steps {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
  background: #ffffff;
}

.step-content {
  text-align: center;
  max-width: 600px;
  width: 100%;
}

.fade-in-out {
  animation: fadeInOut 1s ease-in-out;
}

@keyframes fadeInOut {
  0% {
    opacity: 0;
    transform: translateY(20px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

.happy-image {
  width: 300px;
  height: auto;
  animation: bounce 0.6s ease-in-out;
}

@keyframes bounce {
  0%, 100% {
    transform: translateY(0) scale(1);
  }
  50% {
    transform: translateY(-30px) scale(1.1);
  }
}

.program-title {
  font-size: 1.8rem;
  color: #333333;
  font-weight: 700;
  line-height: 1.4;
  margin: 0;
}

.step-title {
  font-size: 2.5rem;
  color: #667eea;
  font-weight: 700;
  margin: 0;
}

.joke-text {
  font-size: 1.5rem;
  color: #333333;
  font-weight: 600;
  line-height: 1.5;
  margin: 0;
}

.joke-simple {
  max-width: 600px;
}

.joke-line {
  font-size: 1rem;
  color: #333333;
  line-height: 1.8;
  margin: 12px 0;
  text-align: center;
}

.joke-line.highlight {
  color: #667eea;
  font-weight: 600;
  font-style: italic;
}

.joke-punchline {
  font-size: 1.2rem;
  color: #667eea;
  font-weight: 700;
  margin: 20px 0 0 0;
  text-align: center;
}

.transition-text {
  font-size: 1.6rem;
  color: #764ba2;
  font-weight: 600;
  font-style: italic;
  margin: 0;
}

.joke-simple-text {
  font-size: 1.4rem;
  color: #333333;
  font-weight: 600;
  line-height: 1.6;
  margin: 0;
  max-width: 500px;
}

.reaction-image {
  width: 280px;
  height: auto;
  margin: 0 0 30px 0;
}

.hope-text {
  font-size: 1.3rem;
  color: #333333;
  font-weight: 600;
  margin: 0;
}

.compliment-image {
  width: 320px;
  height: auto;
  margin: 0 0 30px 0;
  animation: pulse 1s ease-in-out;
}

@keyframes pulse {
  0%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.05);
  }
}

.compliment-text {
  font-size: 1.1rem;
  color: #56CCF2;
  font-weight: 400;
  margin: 0;
  text-shadow: 2px 2px 4px rgba(86, 204, 242, 0.3);
}

.flowers-image {
  width: 300px;
  height: auto;
  margin: 0 0 40px 0;
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

.invitation-text {
  font-size: 1.8rem;
  color: #333333;
  font-weight: 500;
  margin: 0 0 40px 0;
}

.final-buttons {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 15px;
  width: 100%;
}

.action-button {
  padding: 14px 40px;
  font-size: 0.9rem;
  font-weight: 400;
  border: none;
  border-radius: 50px;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
  width: 80%;
  max-width: 300px;
}

.action-button-yes {
  background: linear-gradient(135deg, #56CCF2 0%, #2F80ED 100%);
  color: #ffffff;
}

.action-button-yes:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
}

.action-button-yes:active {
  transform: translateY(0);
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
}

.action-button-no {
  background: #cccccc;
  color: #999999;
  cursor: not-allowed;
  opacity: 0.6;
}

.action-button-no:disabled {
  cursor: not-allowed;
}

/* Mobile First подход */
@media (min-width: 768px) {
  .happy-image {
    width: 400px;
  }

  .program-title {
    font-size: 2.2rem;
  }

  .step-title {
    font-size: 3rem;
  }

  .joke-text {
    font-size: 1.8rem;
  }

  .joke-line {
    font-size: 1.2rem;
  }

  .joke-punchline {
    font-size: 1.4rem;
  }

  .transition-text {
    font-size: 2rem;
  }

  .joke-simple-text {
    font-size: 1.7rem;
  }

  .reaction-image {
    width: 350px;
  }

  .hope-text {
    font-size: 1.6rem;
  }

  .compliment-image {
    width: 400px;
  }

  .compliment-text {
    font-size: 1.3rem;
  }

  .joke-punchline {
    font-size: 1.4rem;
  }

  .flowers-image {
    width: 400px;
  }

  .invitation-text {
    font-size: 2.2rem;
  }

  .action-button {
    padding: 16px 50px;
    font-size: 1rem;
    max-width: 350px;
  }
}

@media (min-width: 1024px) {
  .happy-image {
    width: 500px;
  }

  .program-title {
    font-size: 2.5rem;
  }

  .step-title {
    font-size: 3.5rem;
  }

  .joke-text {
    font-size: 2rem;
  }

  .joke-line {
    font-size: 1.4rem;
  }

  .joke-punchline {
    font-size: 1.6rem;
  }

  .transition-text {
    font-size: 2.2rem;
  }

  .joke-simple-text {
    font-size: 2rem;
  }

  .reaction-image {
    width: 400px;
  }

  .hope-text {
    font-size: 1.8rem;
  }

  .compliment-image {
    width: 450px;
  }

  .compliment-text {
    font-size: 1.5rem;
  }

  .joke-punchline {
    font-size: 1.6rem;
  }

  .flowers-image {
    width: 500px;
  }

  .invitation-text {
    font-size: 2.5rem;
  }

  .action-button {
    padding: 18px 60px;
    font-size: 1.1rem;
    max-width: 400px;
  }
}
</style>
