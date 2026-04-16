<script setup>
import { ref } from 'vue'

const props = defineProps({
  term: { type: String, required: true }
})

const open = ref(false)

const glossary = {
  'SecAgg+': {
    title: 'Secure Aggregation Plus (SecAgg+)',
    body: `Each hospital splits its weight update into <strong>secret shares</strong> distributed among the other participants. Only the <strong>combined sum</strong> can be reconstructed by the SuperLink.<br/><br/>This means the analyst running the SuperLink can never inspect what any single hospital contributed. They only see the final aggregate.<br/><br/>Requires at least <strong>3 participants</strong>. In dsFlower, SecAgg+ is enforced at both the server side (Flower's SecAggPlusWorkflow) and the client side (secaggplus_mod) as defense-in-depth. XGBoost requires SecAgg+ by design.`
  },
  'DP-SGD': {
    title: 'Differential Privacy with SGD (DP-SGD)',
    body: `Instead of clipping the overall weight update after training, DP-SGD clips <strong>each individual patient's gradient</strong> during training, then adds calibrated Gaussian noise.<br/><br/>This provides <strong>formal (ε, δ)-differential privacy</strong>: a mathematical bound on how much information any single patient contributes to the model. Implemented via <strong>Opacus</strong> (Meta's PyTorch DP library).<br/><br/>Only available for <strong>PyTorch</strong> models. Validated for MLP, LogReg, Linear, Multiclass, Multilabel, and Poisson. Has a higher accuracy cost than update noise, but provides provable guarantees.<br/><br/>The privacy budget (ε/δ) is tracked per-dataset in a persistent ledger on the server. Once exhausted, no more training is allowed.`
  },
  'Update noise': {
    title: 'Update-Level Noise',
    body: `After local training, the <strong>weight delta</strong> (new weights minus old weights) is clipped by its L2 norm, and <strong>Gaussian noise</strong> is added before sending to the SuperLink.<br/><br/>This provides meaningful obfuscation but <strong>no formal DP guarantee</strong>. The noise scale is calibrated from epsilon/delta parameters, but without the per-sample accounting that makes DP-SGD formally private.<br/><br/>Works with <strong>any framework</strong> (sklearn, PyTorch, XGBoost) because it operates on the weight delta, not on individual gradients. Lighter accuracy cost than DP-SGD.<br/><br/>Use when you want practical privacy without the overhead and accuracy loss of formal DP.`
  },
  'Bucketed counts': {
    title: 'Bucketed Counts',
    body: `When hospitals report how many samples they used for training, the exact count is rounded to the <strong>nearest power of 2</strong> before the analyst sees it.<br/><br/>Examples: 847 patients → reported as <strong>1024</strong>. 623 → <strong>512</strong>. 1245 → <strong>1024</strong>.<br/><br/>This prevents the analyst from knowing the exact dataset size of each hospital, which could otherwise be used for re-identification or membership inference attacks.<br/><br/>Applied in all clinical privacy profiles. Only sandbox_open allows exact counts.`
  },
  'Suppressed metrics': {
    title: 'Suppressed Per-Node Metrics',
    body: `In clinical profiles, training metrics like loss, accuracy, or F1 score are reported <strong>only as aggregates across all hospitals</strong>, never individually.<br/><br/>If the analyst could see each hospital's loss separately, they might infer properties of that hospital's data (e.g., unusually high loss → small or atypical population). This is a form of <strong>membership inference</strong> attack.<br/><br/>Implementation: each client returns <strong>loss: 0.0</strong> (dummy) when per-node metrics are suppressed. The server aggregates only the combined result, which remains meaningful while individual values are hidden.`
  },
  'FedAvg / FedProx / FedOpt': {
    title: 'Federated Aggregation Strategies',
    body: `<strong>FedAvg</strong> (Federated Averaging): the SuperLink computes a weighted mean of all hospitals' model weights, proportional to their dataset sizes. Simple, effective when data distributions are similar across sites.<br/><br/><strong>FedProx</strong>: like FedAvg but adds a proximal penalty that prevents each hospital's model from diverging too far from the global model during local training. Essential when hospitals have <strong>non-IID data</strong> (e.g., different patient demographics, different disease prevalences).<br/><br/><strong>FedOpt</strong> (FedAdam, FedAdagrad): the SuperLink applies an <strong>adaptive optimizer</strong> (Adam or Adagrad) to the aggregated updates instead of simple averaging. Helps when training is unstable or features are sparse.<br/><br/><strong>FedBN</strong>: excludes BatchNorm parameters from aggregation. Each hospital keeps its own normalization statistics. Designed for medical imaging where different scanners produce different intensity distributions.`
  },
  'Secure histogram': {
    title: 'Secure Histogram Aggregation (XGBoost)',
    body: `XGBoost builds <strong>decision trees</strong>, not neural networks. It cannot exchange model weights like PyTorch or sklearn. Instead, dsFlower uses a histogram-based protocol.<br/><br/>Each hospital computes <strong>gradient and Hessian histograms</strong> per feature. These are quantized to <strong>int64</strong> (multiplied by 1,000,000) so they can be aggregated with SecAgg+ (which works on integers).<br/><br/>The SuperLink receives only the <strong>summed histograms</strong> from all hospitals and selects the optimal tree split point. No individual hospital's histogram is ever visible.<br/><br/>The process repeats for each node in each tree. SecAgg+ is <strong>mandatory</strong> for XGBoost in dsFlower.`
  },
  'Trust profiles': {
    title: 'Trust Profiles',
    body: `Privacy levels configured by the <strong>server administrator</strong> in the DataSHIELD settings of each hospital. They range from:<br/><br/><strong>sandbox_open</strong>: development only, minimal restrictions, exact counts allowed.<br/><strong>clinical_default</strong>: recommended for hospital deployment. SecAgg+ required, per-node metrics suppressed, counts bucketed.<br/><strong>high_sensitivity_dp</strong>: formal DP-SGD with Opacus, 500+ sample minimum, privacy budget tracking.<br/><br/>In a multi-site federation, the <strong>most restrictive profile</strong> across all servers is automatically adopted by all. The analyst <strong>cannot bypass or downgrade</strong> the profile. This is enforced server-side in the manifest written before SuperNode launch.`
  },
  'Disclosure control': {
    title: 'Disclosure Control',
    body: `A combination of server-enforced measures to prevent information leakage:<br/><br/><strong>Bucketed counts</strong>: sample sizes rounded to nearest power of 2 (847 → 1024).<br/><br/><strong>Suppressed per-node metrics</strong>: individual hospital loss/accuracy hidden, only the aggregate is reported.<br/><br/><strong>Minimum sample sizes</strong>: training blocked if a hospital has fewer patients than the profile threshold (e.g., 100 for clinical_default, 500 for high_sensitivity_dp).<br/><br/><strong>Class distribution checks</strong>: ensures minimum positive examples per class to prevent trivial inference (e.g., if only 2 patients have the target condition, a model could memorize them).`
  }
}

const entry = glossary[props.term] || { title: props.term, body: 'Definition not found.' }

function closeBackdrop(e) {
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
      @click="closeBackdrop"
      style="position: fixed; inset: 0; background: rgba(0,0,0,0.65); z-index: 1000; display: flex; align-items: center; justify-content: center; backdrop-filter: blur(4px); -webkit-backdrop-filter: blur(4px);"
    >
      <div style="background: linear-gradient(135deg, rgba(20,14,10,0.98), rgba(30,20,14,0.98)); border: 1px solid rgba(255,208,0,0.15); border-radius: 16px; max-width: 580px; width: 92%; padding: 2em 2.4em; position: relative; box-shadow: 0 12px 48px rgba(0,0,0,0.5);">
        <button
          @click="open = false"
          style="position: absolute; top: 14px; right: 18px; background: none; border: none; color: #888; font-size: 1.5em; cursor: pointer; line-height: 1; transition: color 0.2s;"
          @mouseenter="$event.target.style.color='#e0d8d0'"
          @mouseleave="$event.target.style.color='#888'"
        >&times;</button>
        <div style="color: #FFD000; font-family: 'Roboto Mono', monospace; font-size: 1.15em; font-weight: 600; margin-bottom: 1em; padding-right: 1.5em;">{{ entry.title }}</div>
        <div style="color: #d8d0c8; font-family: 'Montserrat', sans-serif; font-size: 0.95em; line-height: 1.85;" v-html="entry.body" />
      </div>
    </div>
  </Teleport>
</template>
