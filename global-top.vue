<script setup>
import { ref, onMounted, onUnmounted, computed, watch } from 'vue'
import { useNav } from '@slidev/client'

const { currentPage, total } = useNav()

// Reset demo slide when navigating backward past it
watch(currentPage, (newPage, oldPage) => {
  if (oldPage > newPage && window.__demoResetFn) {
    window.__demoResetFn()
  }
})

// ── Global glossary popup (works inside markdown tables) ──
const glossaryOpen = ref(false)
const glossaryTitle = ref('')
const glossaryBody = ref('')

const glossaryMap = {
  'SecAgg+': { title: 'Secure Aggregation Plus (SecAgg+)', body: `Each hospital splits its weight update into <strong>secret shares</strong> distributed among the other participants. Only the <strong>combined sum</strong> can be reconstructed by the SuperLink.<br/><br/>This means the analyst running the SuperLink can never inspect what any single hospital contributed. They only see the final aggregate.<br/><br/>Requires at least <strong>3 participants</strong>. In dsFlower, SecAgg+ is enforced at both the server side (Flower's SecAggPlusWorkflow) and the client side (secaggplus_mod) as defense-in-depth.` },
  'DP-SGD': { title: 'Differential Privacy with SGD (DP-SGD)', body: `Per-sample gradient clipping + calibrated noise during training, via <strong>Opacus</strong> (Meta). Each patient's gradient is clipped individually, then noise is added.<br/><br/>Provides formal <strong>(ε, δ)-differential privacy</strong>: a mathematical bound on how much any single patient contributes to the model.<br/><br/>Only for <strong>PyTorch</strong> models. The privacy budget (ε/δ) is tracked per-dataset in a persistent ledger on the server.` },
  'Opacus': { title: 'Opacus (DP-SGD Engine)', body: `<strong>Opacus</strong> is Meta's open-source library for training PyTorch models with <strong>differential privacy</strong>.<br/><br/>It wraps the model, optimizer, and dataloader to automatically clip per-sample gradients and add calibrated noise. Provides formal (ε, δ)-DP guarantees with a built-in privacy accountant.<br/><br/>In dsFlower, Opacus is used in the <strong>high_sensitivity_dp</strong> profile. It replaces incompatible layers automatically (e.g., BatchNorm → GroupNorm).` },
  'noise': { title: 'Update-Level Noise', body: `After local training, the <strong>weight delta</strong> is clipped by L2 norm and <strong>Gaussian noise</strong> is added before sending to the SuperLink.<br/><br/>Provides meaningful obfuscation but <strong>no formal DP guarantee</strong>. Works with any framework (sklearn, PyTorch, XGBoost). Lighter accuracy cost than DP-SGD.<br/><br/>Used in the <strong>clinical_update_noise</strong> profile.` },
  'SecAgg': { title: 'Secure Aggregation Plus (SecAgg+)', body: `Each hospital splits its weight update into <strong>secret shares</strong> distributed among the other participants. Only the <strong>combined sum</strong> can be reconstructed.<br/><br/>The analyst running the SuperLink can never inspect what any single hospital contributed. Requires <strong>3+ participants</strong>. Mandatory for XGBoost (secure histogram aggregation).` },
}

function onGlossaryClick(e) {
  const el = e.target.closest('.g-term')
  if (!el) return
  const term = el.dataset.g
  const entry = glossaryMap[term]
  if (entry) {
    glossaryTitle.value = entry.title
    glossaryBody.value = entry.body
    glossaryOpen.value = true
  }
}

function closeGlossary(e) {
  if (e.target === e.currentTarget) glossaryOpen.value = false
}

onMounted(() => document.addEventListener('click', onGlossaryClick))
onUnmounted(() => document.removeEventListener('click', onGlossaryClick))

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
const showCountdown = computed(() => currentPage.value < total.value)
const isContentSlide = computed(() => currentPage.value > 1 && currentPage.value < total.value)
const contentIndex = computed(() => currentPage.value - 1)
const contentTotal = computed(() => total.value - 2)
</script>

<template>
  <!-- Countdown top-right (content slides only) -->
  <div v-if="showCountdown" class="countdown" :class="{ low: isLow }">
    {{ timeStr }}
  </div>

  <!-- Slide counter bottom-right (content slides only) -->
  <div v-if="isContentSlide" class="slide-counter">
    {{ contentIndex }} / {{ contentTotal }}
  </div>

  <!-- Global glossary popup -->
  <div v-if="glossaryOpen" @click="closeGlossary" class="glossary-backdrop">
    <div class="glossary-modal">
      <button @click="glossaryOpen = false" class="glossary-close">&times;</button>
      <div class="glossary-title">{{ glossaryTitle }}</div>
      <div class="glossary-body" v-html="glossaryBody" />
    </div>
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

.glossary-backdrop {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.65);
  z-index: 1000;
  display: flex;
  align-items: center;
  justify-content: center;
  backdrop-filter: blur(4px);
  -webkit-backdrop-filter: blur(4px);
}

.glossary-modal {
  background: linear-gradient(135deg, rgba(20,14,10,0.98), rgba(30,20,14,0.98));
  border: 1px solid rgba(255,208,0,0.15);
  border-radius: 16px;
  max-width: 580px;
  width: 92%;
  padding: 2em 2.4em;
  position: relative;
  box-shadow: 0 12px 48px rgba(0,0,0,0.5);
}

.glossary-close {
  position: absolute;
  top: 14px;
  right: 18px;
  background: none;
  border: none;
  color: #888;
  font-size: 1.5em;
  cursor: pointer;
  line-height: 1;
  transition: color 0.2s;
}
.glossary-close:hover { color: #e0d8d0; }

.glossary-title {
  color: #FFD000;
  font-family: 'Roboto Mono', monospace;
  font-size: 1.15em;
  font-weight: 600;
  margin-bottom: 1em;
  padding-right: 1.5em;
}

.glossary-body {
  color: #d8d0c8;
  font-family: 'Montserrat', sans-serif;
  font-size: 0.95em;
  line-height: 1.85;
}
.glossary-body :deep(strong) {
  color: #FFD000;
  font-weight: 600;
}
</style>
