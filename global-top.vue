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
  'Disclosure control': { title: 'Disclosure Control', body: `A combination of server-enforced measures to prevent information leakage:<br/><br/><strong>Bucketed counts</strong>: sample sizes rounded to nearest power of 2 (847 → 1024).<br/><br/><strong>Suppressed per-node metrics</strong>: individual hospital loss/accuracy hidden, only the aggregate is reported.<br/><br/><strong>Minimum sample sizes</strong>: training blocked if a hospital has fewer patients than the profile threshold (e.g., 100 for clinical_default).<br/><br/><strong>Class distribution checks</strong>: ensures minimum positive examples per class to prevent trivial inference.` },
  'Trust profiles': { title: 'Trust Profiles', body: `Privacy levels configured by the <strong>server administrator</strong> in the DataSHIELD settings. Range from <strong>sandbox_open</strong> (development, minimal restrictions) to <strong>high_sensitivity_dp</strong> (formal DP-SGD with Opacus, 500+ minimum).<br/><br/>Controls: minimum sample sizes, SecAgg+ requirement, DP mode, metric visibility, exact count reporting, model release policy.<br/><br/>The <strong>most restrictive</strong> profile across all servers is automatically adopted. The analyst <strong>cannot bypass or downgrade</strong> the profile.` },
  'FedAvg / FedProx / FedOpt': { title: 'Federated Aggregation Strategies', body: `<strong>FedAvg</strong>: weighted mean of model weights from all participants, proportional to dataset sizes. Simple, effective when data is similar across sites.<br/><br/><strong>FedProx</strong>: adds a proximal penalty preventing each hospital's model from diverging too far from the global model. Essential for <strong>non-IID data</strong> (different patient populations).<br/><br/><strong>FedOpt</strong> (FedAdam, FedAdagrad): the SuperLink applies an <strong>adaptive optimizer</strong> to aggregated updates instead of simple averaging. Helps with unstable convergence.<br/><br/><strong>FedBN</strong>: excludes BatchNorm from aggregation. Each site keeps its own normalization stats. For medical imaging with different scanners.` },
  'Secure histogram': { title: 'Secure Histogram Aggregation (XGBoost)', body: `XGBoost builds <strong>decision trees</strong>, not neural networks. It cannot exchange weights like PyTorch or sklearn.<br/><br/>Each hospital computes <strong>gradient/Hessian histograms</strong> per feature. These are quantized to <strong>int64</strong> (×1,000,000) for compatibility with SecAgg+.<br/><br/>The SuperLink receives only the <strong>summed histograms</strong> and selects optimal tree splits. Individual hospital contributions are never visible.<br/><br/><strong>SecAgg+ is mandatory</strong> for XGBoost in dsFlower.` },
  'Bucketed counts': { title: 'Bucketed Counts', body: `Sample counts rounded to the <strong>nearest power of 2</strong> before the analyst sees them.<br/><br/>Examples: 847 → <strong>1024</strong>, 623 → <strong>512</strong>, 1245 → <strong>1024</strong>.<br/><br/>Prevents exact dataset size inference. Applied in all clinical privacy profiles. Only sandbox_open reports exact counts.` },
  'Suppressed metrics': { title: 'Suppressed Per-Node Metrics', body: `In clinical profiles, training metrics are reported <strong>only as aggregates</strong>, never per-hospital.<br/><br/>Each client returns <strong>loss: 0.0</strong> (dummy) when per-node metrics are suppressed. The server aggregates only the combined result. Prevents the analyst from inferring properties of individual hospital datasets.` },
  'Update noise': { title: 'Update-Level Noise', body: `After local training, the <strong>weight delta</strong> is clipped by L2 norm and <strong>Gaussian noise</strong> is added.<br/><br/>Provides meaningful obfuscation but <strong>no formal DP guarantee</strong>. Works with any framework (sklearn, PyTorch, XGBoost). Lighter accuracy cost than DP-SGD.<br/><br/>Used in the <strong>clinical_update_noise</strong> profile.` },
  'gRPC/TLS': { title: 'gRPC with TLS Encryption', body: `<strong>gRPC</strong> (Google Remote Procedure Call) is the binary protocol Flower uses for SuperNode ↔ SuperLink communication. It's efficient and supports streaming, but is <strong>not encrypted by default</strong>.<br/><br/>dsFlower generates <strong>ephemeral TLS certificates</strong> (EC P-256) when the SuperLink starts. The CA certificate is passed to each hospital via DataSHIELD, and SuperNodes validate the connection.<br/><br/>This means <strong>all weight exchange is encrypted in transit</strong>. Combined with SecAgg+ (which encrypts the values themselves), there are two layers of protection on the communication channel.` },
  'FedProx': { title: 'FedProx (Federated Proximal)', body: `A variant of FedAvg that adds a <strong>proximal penalty term</strong> to each hospital's local training objective.<br/><br/>The penalty prevents each hospital's model from diverging too far from the current global model. Controlled by <strong>proximal_mu</strong>: higher values = stronger pull toward global model.<br/><br/>Essential for <strong>non-IID data</strong>: when hospitals have different patient populations, disease prevalences, or demographic distributions. Without FedProx, local models can drift apart and aggregation degrades.` },
  'FedAvg': { title: 'FedAvg (Federated Averaging)', body: `The standard federated learning aggregation strategy. Each hospital trains locally, sends its weight updates to the SuperLink, which computes the <strong>weighted mean</strong> proportional to dataset sizes.<br/><br/>Simple and effective when data distributions are <strong>similar across sites</strong>. For heterogeneous data, consider FedProx or FedAdam.` },
}

function onGlossaryClick(e) {
  const el = e.target.closest('.g-term') || (e.target.classList?.contains('g-term') ? e.target : null)
  if (!el) return
  const term = el.dataset?.g || el.getAttribute('data-g')
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
