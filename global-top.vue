<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue'
import { useNav } from '@slidev/client'

const { currentPage, total } = useNav()

// Countdown: 10 minutes
const totalSeconds = ref(10 * 60)
let timer = null

onMounted(() => {
  timer = setInterval(() => {
    if (totalSeconds.value > 0) totalSeconds.value--
  }, 1000)
})

onUnmounted(() => clearInterval(timer))

const minutes = computed(() => Math.floor(totalSeconds.value / 60))
const seconds = computed(() => totalSeconds.value % 60)
const timeStr = computed(() =>
  `${String(minutes.value).padStart(2, '0')}:${String(seconds.value).padStart(2, '0')}`
)
const isLow = computed(() => totalSeconds.value < 60)

// Slide counter: exclude cover (1) and closing (last)
const showUI = computed(() => currentPage.value > 1 && currentPage.value < total.value)
const isContentSlide = computed(() => currentPage.value > 1 && currentPage.value < total.value)
const contentIndex = computed(() => currentPage.value - 1)
const contentTotal = computed(() => total.value - 2)
</script>

<template>
  <!-- Countdown top-right (content slides only) -->
  <div v-if="showUI" class="countdown" :class="{ low: isLow }">
    {{ timeStr }}
  </div>

  <!-- Slide counter bottom-right (content slides only) -->
  <div v-if="showUI" class="slide-counter">
    {{ contentIndex }} / {{ contentTotal }}
  </div>
</template>

<style scoped>
.countdown {
  position: fixed;
  top: 16px;
  right: 20px;
  font-family: 'Roboto Mono', monospace;
  font-size: 14px;
  font-weight: 500;
  color: rgba(255, 255, 255, 0.5);
  z-index: 100;
  letter-spacing: 0.05em;
}

.countdown.low {
  color: rgba(255, 80, 60, 0.8);
}

.slide-counter {
  position: fixed;
  bottom: 16px;
  right: 20px;
  font-family: 'Roboto Mono', monospace;
  font-size: 13px;
  font-weight: 400;
  color: rgba(255, 255, 255, 0.4);
  z-index: 100;
  letter-spacing: 0.05em;
}
</style>
