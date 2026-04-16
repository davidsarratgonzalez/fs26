<script setup>
import { ref } from 'vue'

const props = defineProps({
  term: { type: String, required: true }
})

const open = ref(false)

const glossary = {
  'SecAgg+': {
    title: 'Secure Aggregation Plus (SecAgg+)',
    body: `Encrypts individual weight updates via secret sharing so the SuperLink (analyst) only sees the <strong>aggregate</strong>, never any single hospital's contribution.\n\nEach participant splits its update into secret shares distributed among peers. Only the combined sum can be reconstructed. Requires 3+ participants.\n\nIn dsFlower, SecAgg+ is enforced at both server-side (Flower SecAggPlusWorkflow) and client-side (secaggplus_mod) as defense-in-depth.`
  },
  'DP-SGD': {
    title: 'Differential Privacy with SGD (DP-SGD)',
    body: `Per-sample gradient clipping + calibrated noise during training, implemented via <strong>Opacus</strong> (Meta). Each patient's gradient is clipped individually before aggregation, then noise is added.\n\nProvides formal <strong>(ε, δ)-differential privacy</strong> guarantees: mathematically bounded information leakage per patient.\n\nOnly available for PyTorch models. Validated for: MLP, LogReg, Linear, Multiclass, Multilabel, Poisson.\n\n<em>Compare with Update noise: DP-SGD is per-sample (formal guarantee), update noise is per-update (no formal guarantee).</em>`
  },
  'Update noise': {
    title: 'Update-Level Noise',
    body: `After local training, the <strong>weight delta</strong> (new weights - old weights) is clipped by L2 norm and <strong>Gaussian noise</strong> is added.\n\nProvides meaningful obfuscation but <strong>NO formal DP guarantee</strong>. The noise scale is calibrated from epsilon/delta parameters but without per-sample accounting.\n\nWorks with <strong>any framework</strong> (sklearn, PyTorch, XGBoost). Lighter impact on model accuracy than DP-SGD.\n\n<em>Use when you want practical privacy without the accuracy cost of formal DP.</em>`
  },
  'Bucketed counts': {
    title: 'Bucketed Counts',
    body: `Sample counts are rounded to the <strong>nearest power of 2</strong> before being reported to the analyst.\n\nExamples: 847 → 1024, 623 → 512, 1245 → 1024\n\nPrevents the analyst from inferring exact dataset sizes, which could be used for re-identification or membership inference attacks.\n\nApplied in all clinical privacy profiles. Only sandbox_open reports exact counts.`
  },
  'Suppressed metrics': {
    title: 'Suppressed Per-Node Metrics',
    body: `In clinical profiles, training metrics (loss, accuracy, F1, etc.) are reported <strong>only as aggregates</strong>, never per-hospital.\n\nIf per-node loss were visible, the analyst could infer properties of individual hospital datasets (e.g., one hospital has much higher loss → smaller or unusual population).\n\nImplementation: each client returns <strong>loss: 0.0</strong> (dummy value) when allow_per_node_metrics = FALSE. The server aggregates only the combined result.`
  },
  'FedAvg / FedProx / FedOpt': {
    title: 'Federated Aggregation Strategies',
    body: `<strong>FedAvg</strong> (Federated Averaging): weighted mean of model weights from all participants. Simple, effective when data is similar across sites.\n\n<strong>FedProx</strong>: adds a proximal penalty that prevents each hospital's model from diverging too far from the global model. Essential for <strong>non-IID data</strong> (different patient populations).\n\n<strong>FedOpt</strong> (FedAdam, FedAdagrad): the server applies an <strong>adaptive optimizer</strong> (Adam or Adagrad) to the aggregated updates instead of simple averaging. Improves convergence in unstable scenarios.\n\n<strong>FedBN</strong>: excludes BatchNorm parameters from aggregation. Each site keeps its own normalization stats. For medical imaging with different scanners.`
  },
  'Secure histogram': {
    title: 'Secure Histogram Aggregation (XGBoost)',
    body: `XGBoost builds decision trees, not neural networks. It can't exchange "weights" like PyTorch/sklearn.\n\nInstead, each hospital computes <strong>gradient/Hessian histograms</strong> per feature. These are <strong>quantized to int64</strong> (×1,000,000) for compatibility with SecAgg+.\n\nThe server receives only the <strong>aggregated</strong> histograms and selects the optimal tree split. Individual hospital contributions are never visible.\n\n<strong>SecAgg+ is mandatory</strong> for XGBoost in dsFlower.`
  },
  'Trust profiles': {
    title: 'Trust Profiles',
    body: `Server-admin configured privacy levels in DataSHIELD settings. Range from <strong>sandbox_open</strong> (development, minimal restrictions) to <strong>high_sensitivity_dp</strong> (formal DP-SGD with Opacus).\n\nControls: minimum sample sizes, SecAgg+ requirement, DP mode, metric visibility, exact count reporting, model release policy.\n\nThe <strong>most restrictive</strong> profile across all servers in a federation is automatically adopted by all. The analyst <strong>cannot</strong> bypass or downgrade the profile.`
  },
  'Disclosure control': {
    title: 'Disclosure Control',
    body: `A combination of measures to prevent information leakage:\n\n<strong>Bucketed counts</strong>: sample sizes rounded to nearest power of 2 (847 → 1024).\n\n<strong>Suppressed per-node metrics</strong>: individual hospital loss/accuracy hidden, only aggregate reported.\n\n<strong>Minimum sample sizes</strong>: training blocked if a hospital has fewer than the profile threshold (e.g., 100 for clinical_default).\n\n<strong>Class distribution checks</strong>: ensures minimum positive examples per class to prevent trivial inference.`
  }
}

const entry = glossary[props.term] || { title: props.term, body: 'Definition not found.' }

function close(e) {
  if (e.target === e.currentTarget) open.value = false
}
</script>

<template>
  <span
    @click.stop="open = true"
    style="cursor: pointer; border-bottom: 1px dotted currentColor; padding-bottom: 1px;"
  >{{ term }}</span>

  <Teleport to="body">
    <div
      v-if="open"
      @click="close"
      style="position: fixed; inset: 0; background: rgba(0,0,0,0.6); z-index: 1000; display: flex; align-items: center; justify-content: center;"
    >
      <div style="background: rgba(15,10,8,0.97); border: 1px solid rgba(255,255,255,0.15); border-radius: 14px; max-width: 520px; width: 90%; padding: 1.5em 2em; position: relative; box-shadow: 0 8px 32px rgba(0,0,0,0.4);">
        <button
          @click="open = false"
          style="position: absolute; top: 12px; right: 16px; background: none; border: none; color: #888; font-size: 1.3em; cursor: pointer; line-height: 1;"
        >&times;</button>
        <div style="color: #FFD000; font-family: 'Roboto Mono', monospace; font-size: 1.05em; font-weight: 600; margin-bottom: 0.8em;">{{ entry.title }}</div>
        <div style="color: #d8d0c8; font-size: 0.88em; line-height: 1.7; white-space: pre-line;" v-html="entry.body.replace(/\n/g, '<br/>')" />
      </div>
    </div>
  </Teleport>
</template>
