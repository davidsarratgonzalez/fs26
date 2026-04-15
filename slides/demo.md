<script setup>
import { ref, onMounted, onActivated, nextTick } from 'vue'
import { useSlideContext } from '@slidev/client'

const terminal = ref(null)
const slideCtx = useSlideContext()
let debounce = null

function resetDemo() {
  slideCtx.$clicks.value = 0
  nextTick(() => {
    nextTick(() => {
      if (terminal.value) {
        terminal.value.scrollTop = 0
        // Force-reset animations via reflow trick
        terminal.value.querySelectorAll('.exec-lines > div').forEach(el => {
          el.style.opacity = ''
          el.style.animationName = 'none'
          void el.offsetHeight
          el.style.animationName = ''
        })
      }
    })
  })
}

onActivated(() => resetDemo())
window.__demoResetFn = resetDemo

onMounted(() => {
  if (!terminal.value) return
  terminal.value.scrollTop = 0
  const observer = new MutationObserver(() => {
    clearTimeout(debounce)
    debounce = setTimeout(() => {
      if (!terminal.value) return
      const inner = terminal.value.firstElementChild
      if (!inner) return
      const visible = Array.from(inner.children).filter(
        el => !el.classList.contains('slidev-vclick-hidden')
      )
      const last = visible[visible.length - 1]
      if (last) {
        last.scrollIntoView({ behavior: 'smooth', block: 'end' })
      }
    }, 120)
  })
  observer.observe(terminal.value, {
    subtree: true, attributes: true, attributeFilter: ['class']
  })
})
</script>

## Usage Demo

<div ref="terminal" style="overflow-y: auto; scroll-behavior: smooth; height: 430px; margin-top: 0.3em; scrollbar-width: none;">
<div style="font-size: 0.62em; line-height: 1.4; font-family: 'Roboto Mono', monospace;">

<!-- Experiment setup -->
<div style="background: rgba(136,204,255,0.04); border: 1px solid rgba(136,204,255,0.12); border-radius: 10px; padding: 0.8em 1.2em; margin-bottom: 10px;">

<div style="color: #88ccff; font-size: 1.2em; font-weight: 600; margin-bottom: 10px;">Federated ICU Mortality Prediction</div>

<!-- Hospitals grid -->
<div style="display: flex; gap: 8px; margin-bottom: 12px;">
  <div style="flex:1; background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.10); border-radius: 8px; padding: 8px 10px; text-align: center;">
    <div style="color: #FFD000; font-weight: 600; font-size: 1.05em;">BCN</div>
    <div style="color: #c8c0b8; font-size: 0.85em;">Hospital Clinic</div>
    <div style="color: #88ccff; font-size: 0.9em; margin-top: 2px;">2,341</div>
  </div>
  <div style="flex:1; background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.10); border-radius: 8px; padding: 8px 10px; text-align: center;">
    <div style="color: #FFD000; font-weight: 600; font-size: 1.05em;">MAD</div>
    <div style="color: #c8c0b8; font-size: 0.85em;">La Paz</div>
    <div style="color: #88ccff; font-size: 0.9em; margin-top: 2px;">1,876</div>
  </div>
  <div style="flex:1; background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.10); border-radius: 8px; padding: 8px 10px; text-align: center;">
    <div style="color: #FFD000; font-weight: 600; font-size: 1.05em;">LDN</div>
    <div style="color: #c8c0b8; font-size: 0.85em;">King's College</div>
    <div style="color: #88ccff; font-size: 0.9em; margin-top: 2px;">3,102</div>
  </div>
  <div style="flex:1; background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.10); border-radius: 8px; padding: 8px 10px; text-align: center;">
    <div style="color: #FFD000; font-weight: 600; font-size: 1.05em;">BER</div>
    <div style="color: #c8c0b8; font-size: 0.85em;">Charit&eacute;</div>
    <div style="color: #88ccff; font-size: 0.9em; margin-top: 2px;">1,245</div>
  </div>
  <div style="flex:1; background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.10); border-radius: 8px; padding: 8px 10px; text-align: center;">
    <div style="color: #FFD000; font-weight: 600; font-size: 1.05em;">AMS</div>
    <div style="color: #c8c0b8; font-size: 0.85em;">AMC</div>
    <div style="color: #88ccff; font-size: 0.9em; margin-top: 2px;">2,567</div>
  </div>
</div>

<!-- Dataset + Features -->
<div style="display: flex; gap: 16px; margin-bottom: 10px;">
  <div style="flex: 1;">
    <div style="color: #ffb366; font-weight: 500; margin-bottom: 3px;">Dataset</div>
    <div style="color: #e0d8d0;">ICU.admissions</div>
    <div style="color: #b8b0a8; font-size: 0.9em;">11,131 patients total (data never pooled)</div>
  </div>
  <div style="flex: 1;">
    <div style="color: #ffb366; font-weight: 500; margin-bottom: 5px;">Target</div>
    <div style="margin-bottom: 6px;"><span style="background:rgba(102,221,170,0.12); border:1px solid rgba(102,221,170,0.25); border-radius:4px; padding:3px 10px; color:#66ddaa;">icu_mortality</span></div>
    <div style="color: #c8c0b8; font-size: 0.9em;">binary &middot; 14.2% prevalence</div>
  </div>
</div>

<!-- Features -->
<div style="margin-bottom: 10px;">
  <div style="color: #ffb366; font-weight: 500; margin-bottom: 4px;">Features <span style="color: #c8c0b8; font-weight: 400;">(17 clinical variables)</span></div>
  <div style="display: flex; flex-wrap: wrap; gap: 4px;">
    <span style="background:rgba(255,208,0,0.10); border:1px solid rgba(255,208,0,0.18); border-radius:4px; padding:2px 7px; color:#FFD000;">age</span>
    <span style="background:rgba(255,208,0,0.10); border:1px solid rgba(255,208,0,0.18); border-radius:4px; padding:2px 7px; color:#FFD000;">heart_rate</span>
    <span style="background:rgba(255,208,0,0.10); border:1px solid rgba(255,208,0,0.18); border-radius:4px; padding:2px 7px; color:#FFD000;">systolic_bp</span>
    <span style="background:rgba(255,208,0,0.10); border:1px solid rgba(255,208,0,0.18); border-radius:4px; padding:2px 7px; color:#FFD000;">spo2</span>
    <span style="background:rgba(255,208,0,0.10); border:1px solid rgba(255,208,0,0.18); border-radius:4px; padding:2px 7px; color:#FFD000;">creatinine</span>
    <span style="background:rgba(255,208,0,0.10); border:1px solid rgba(255,208,0,0.18); border-radius:4px; padding:2px 7px; color:#FFD000;">lactate</span>
    <span style="background:rgba(255,208,0,0.10); border:1px solid rgba(255,208,0,0.18); border-radius:4px; padding:2px 7px; color:#FFD000;">gcs</span>
    <span style="background:rgba(255,208,0,0.10); border:1px solid rgba(255,208,0,0.18); border-radius:4px; padding:2px 7px; color:#FFD000;">ventilation</span>
    <span style="color:#b0a8a0; display:inline-flex; align-items:center; height:22px;">+9 more</span>
  </div>
</div>

<!-- Model config -->
<div style="display: flex; gap: 20px; padding-top: 6px; border-top: 1px solid rgba(255,255,255,0.06);">
  <div>
    <span style="color:#88ccff; font-weight: 500;">Model</span>
    <span style="color:#e0d8d0; margin-left: 6px;">PyTorch MLP (128-64-32)</span>
  </div>
  <div>
    <span style="color:#88ccff; font-weight: 500;">Strategy</span>
    <span style="color:#e0d8d0; margin-left: 6px;">FedProx</span>
  </div>
  <div>
    <span style="color:#88ccff; font-weight: 500;">Rounds</span>
    <span style="color:#e0d8d0; margin-left: 6px;">10</span>
  </div>
</div>

</div>

<!-- Libraries -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; color: #c8b8a8;">
<span style="color:#78a9ff;">library</span>(<span style="color:#FFD000;">DSI</span>); <span style="color:#78a9ff;">library</span>(<span style="color:#FFD000;">DSOpal</span>); <span style="color:#78a9ff;">library</span>(<span style="color:#FFD000;">dsFlowerClient</span>)
</div>

<!-- Login -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
builder <span style="color:#b0a8a0;">&lt;-</span> DSI::<span style="color:#78a9ff;">newDSLoginBuilder</span>()
<br/>builder$<span style="color:#78a9ff;">append</span>(server = <span style="color:#ffaacc;">"BCN"</span>, url = <span style="color:#ffaacc;">"https://datashield.clinic.cat"</span>, table = <span style="color:#ffaacc;">"ICU.admissions"</span>, <span style="color:#666;">...</span>) <span style="color:#666;"># + credentials</span>
<br/>builder$<span style="color:#78a9ff;">append</span>(server = <span style="color:#ffaacc;">"MAD"</span>, url = <span style="color:#ffaacc;">"https://datashield.lapaz.salud.es"</span>, table = <span style="color:#ffaacc;">"ICU.admissions"</span>, <span style="color:#666;">...</span>)
<br/>builder$<span style="color:#78a9ff;">append</span>(server = <span style="color:#ffaacc;">"LDN"</span>, url = <span style="color:#ffaacc;">"https://datashield.kcl.nhs.uk"</span>, table = <span style="color:#ffaacc;">"ICU.admissions"</span>, <span style="color:#666;">...</span>)
<br/>builder$<span style="color:#78a9ff;">append</span>(server = <span style="color:#ffaacc;">"BER"</span>, url = <span style="color:#ffaacc;">"https://datashield.charite.de"</span>, table = <span style="color:#ffaacc;">"ICU.admissions"</span>, <span style="color:#666;">...</span>)
<br/>builder$<span style="color:#78a9ff;">append</span>(server = <span style="color:#ffaacc;">"AMS"</span>, url = <span style="color:#ffaacc;">"https://datashield.amsterdamumc.nl"</span>, table = <span style="color:#ffaacc;">"ICU.admissions"</span>, <span style="color:#666;">...</span>)
<br/>conns <span style="color:#b0a8a0;">&lt;-</span> DSI::<span style="color:#78a9ff;">datashield.login</span>(logins = builder$<span style="color:#78a9ff;">build</span>(), assign = <span style="color:#88ccff;">TRUE</span>, symbol = <span style="color:#ffaacc;">"D"</span>)
</div>

<div v-click class="exec-lines" style="background: rgba(15,10,8,0.5); border-left: 3px solid #444; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin: 2px 0; color: #b8b0a8;">
<div style="animation-delay:0.2s">Logging into the collaborating servers</div>
<div style="animation-delay:1.2s">&nbsp; Login BCN: <span style="color:#66ddaa;">OK</span></div>
<div style="animation-delay:2.5s">&nbsp; Login MAD: <span style="color:#66ddaa;">OK</span></div>
<div style="animation-delay:4.0s">&nbsp; Login LDN: <span style="color:#66ddaa;">OK</span></div>
<div style="animation-delay:5.2s">&nbsp; Login BER: <span style="color:#66ddaa;">OK</span></div>
<div style="animation-delay:6.1s">&nbsp; Login AMS: <span style="color:#66ddaa;">OK</span></div>
<div style="animation-delay:6.4s">Assigned table ICU.admissions to symbol "D"</div>
</div>

<!-- Connect -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
flower <span style="color:#b0a8a0;">&lt;-</span> <span style="color:#78a9ff;">ds.flower.connect</span>(conns, symbol = <span style="color:#ffaacc;">"D"</span>)
</div>

<div v-click class="exec-lines" style="background: rgba(15,10,8,0.5); border-left: 3px solid #444; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin: 2px 0; color: #b8b0a8;">
<div style="animation-delay:0.3s">Initializing dsFlower federation on 5 servers...</div>
<div style="animation-delay:0.8s">&nbsp; BCN: dsFlower v0.1.0 <span style="color:#b0a8a0;">(2,341 rows x 17 cols)</span></div>
<div style="animation-delay:1.2s">&nbsp; MAD: dsFlower v0.1.0 <span style="color:#b0a8a0;">(1,876 rows x 17 cols)</span></div>
<div style="animation-delay:1.7s">&nbsp; LDN: dsFlower v0.1.0 <span style="color:#b0a8a0;">(3,102 rows x 17 cols)</span></div>
<div style="animation-delay:2.1s">&nbsp; BER: dsFlower v0.1.0 <span style="color:#b0a8a0;">(1,245 rows x 17 cols)</span></div>
<div style="animation-delay:2.4s">&nbsp; AMS: dsFlower v0.1.0 <span style="color:#b0a8a0;">(2,567 rows x 17 cols)</span></div>
<div style="animation-delay:2.8s">&nbsp; Total: <span style="color:#e0d8d0;">11,131 patients</span> across 5 sites (data never pooled)</div>
<div style="animation-delay:3.1s">&nbsp; Trust profile: <span style="color:#66ddaa;">clinical_default</span> (SecAgg+ required)</div>
</div>

<!-- Recipe -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
recipe <span style="color:#b0a8a0;">&lt;-</span> <span style="color:#78a9ff;">ds.flower.recipe</span>(
<br/>&nbsp;&nbsp;model &nbsp;&nbsp;&nbsp;&nbsp;= ds.flower.model.<span style="color:#FFD000;">pytorch_mlp</span>(
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;hidden_layers = <span style="color:#ffaacc;">"128,64,32"</span>,
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;learning_rate = <span style="color:#88ccff;">0.001</span>,
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;batch_size &nbsp;&nbsp;&nbsp;= <span style="color:#88ccff;">64L</span>,
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;local_epochs &nbsp;= <span style="color:#88ccff;">3L</span>),
<br/>&nbsp;&nbsp;strategy &nbsp;= ds.flower.strategy.<span style="color:#FFD000;">fedprox</span>(proximal_mu = <span style="color:#88ccff;">0.01</span>),
<br/>&nbsp;&nbsp;target_column = <span style="color:#ffaacc;">"icu_mortality"</span>,
<br/>&nbsp;&nbsp;num_rounds &nbsp;&nbsp;&nbsp;= <span style="color:#88ccff;">10L</span>
<br/>)
<br/>result <span style="color:#b0a8a0;">&lt;-</span> <span style="color:#78a9ff;">ds.flower.run</span>(flower, recipe)
</div>

<!-- Run output -->
<div v-click class="exec-lines" style="background: rgba(15,10,8,0.5); border-left: 3px solid #444; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin: 2px 0; color: #b8b0a8;">
<div style="animation-delay:0.8s">SuperLink started (PID: 41823, TLS)</div>
<div style="animation-delay:1.1s">&nbsp; Fleet API: 127.0.0.1:9092</div>
<div style="animation-delay:2.5s">&nbsp; BCN: SuperNode <span style="color:#66ddaa;">connected</span></div>
<div style="animation-delay:3.5s">&nbsp; MAD: SuperNode <span style="color:#66ddaa;">connected</span></div>
<div style="animation-delay:4.8s">&nbsp; LDN: SuperNode <span style="color:#66ddaa;">connected</span></div>
<div style="animation-delay:5.6s">&nbsp; BER: SuperNode <span style="color:#66ddaa;">connected</span></div>
<div style="animation-delay:6.2s">&nbsp; AMS: SuperNode <span style="color:#66ddaa;">connected</span></div>
<div style="animation-delay:7.0s">&nbsp; Code verification <span style="color:#66ddaa;">passed</span> on all servers <span style="color:#b0a8a0;">(app hash matches server templates)</span></div>
<div style="animation-delay:8.5s"><span style="color:#88ccff;">[ROUND &nbsp;1/10]</span> 5 clients &mdash; loss: 0.6814</div>
<div style="animation-delay:10.0s"><span style="color:#88ccff;">[ROUND &nbsp;2/10]</span> 5 clients &mdash; loss: 0.5923</div>
<div style="animation-delay:11.3s"><span style="color:#88ccff;">[ROUND &nbsp;3/10]</span> 5 clients &mdash; loss: 0.5107</div>
<div style="animation-delay:12.6s"><span style="color:#88ccff;">[ROUND &nbsp;4/10]</span> 5 clients &mdash; loss: 0.4489</div>
<div style="animation-delay:13.8s"><span style="color:#88ccff;">[ROUND &nbsp;5/10]</span> 5 clients &mdash; loss: 0.4021</div>
<div style="animation-delay:14.9s"><span style="color:#88ccff;">[ROUND &nbsp;6/10]</span> 5 clients &mdash; loss: 0.3712</div>
<div style="animation-delay:16.0s"><span style="color:#88ccff;">[ROUND &nbsp;7/10]</span> 5 clients &mdash; loss: 0.3498</div>
<div style="animation-delay:17.0s"><span style="color:#88ccff;">[ROUND &nbsp;8/10]</span> 5 clients &mdash; loss: 0.3341</div>
<div style="animation-delay:17.9s"><span style="color:#88ccff;">[ROUND &nbsp;9/10]</span> 5 clients &mdash; loss: 0.3219</div>
<div style="animation-delay:18.8s"><span style="color:#88ccff;">[ROUND 10/10]</span> 5 clients &mdash; loss: 0.3148</div>
<div style="animation-delay:19.3s"><span style="color:#66ddaa;">Model saved to ./dsflower_output/pytorch_mlp_FedProx_10r_20260415</span></div>
<div style="animation-delay:19.6s">SuperLink stopped.</div>
</div>

<!-- Results -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
result$history
</div>

<div v-click style="background: rgba(15,10,8,0.5); border-left: 3px solid #444; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin: 2px 0; color: #b8b0a8;">
&nbsp; round &nbsp;&nbsp;&nbsp;&nbsp;loss &nbsp;&nbsp;&nbsp;n_clients<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 1 &nbsp; 0.6814 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 5<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 2 &nbsp; 0.5923 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 5<br/>
&nbsp;&nbsp;&nbsp; ... &nbsp;&nbsp;&nbsp;&nbsp; ... &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;...<br/>
&nbsp;&nbsp;&nbsp;&nbsp; 10 &nbsp; <span style="color:#FFD000;">0.3148</span> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 5
</div>

<!-- Predict on a real patient -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
<span style="color:#666;"># Predict on a new ICU admission</span>
<br/><span style="color:#666;"># 72yo, tachycardic, hypotensive, elevated lactate, on ventilator</span>
<br/>patient <span style="color:#b0a8a0;">&lt;-</span> <span style="color:#78a9ff;">data.frame</span>(
<br/>&nbsp;&nbsp;age = <span style="color:#88ccff;">72</span>, heart_rate = <span style="color:#88ccff;">112</span>, systolic_bp = <span style="color:#88ccff;">85</span>,
<br/>&nbsp;&nbsp;spo2 = <span style="color:#88ccff;">89</span>, creatinine = <span style="color:#88ccff;">2.4</span>, lactate = <span style="color:#88ccff;">4.1</span>,
<br/>&nbsp;&nbsp;gcs = <span style="color:#88ccff;">10</span>, ventilation = <span style="color:#88ccff;">1</span>, <span style="color:#666;">...</span>)
<br/><span style="color:#78a9ff;">ds.flower.predict</span>(result, newdata = patient, type = <span style="color:#ffaacc;">"prob"</span>)
</div>

<div v-click style="background: rgba(15,10,8,0.5); border-left: 3px solid #444; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin: 2px 0; color: #b8b0a8;">
[1] <span style="color:#FFD000;">0.7321</span> <span style="color:#b0a8a0;">&nbsp;&nbsp;# 73% ICU mortality risk</span>
</div>

<!-- Disconnect -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
<span style="color:#78a9ff;">ds.flower.disconnect</span>(flower)
<br/>DSI::<span style="color:#78a9ff;">datashield.logout</span>(conns)
</div>

<div v-click class="exec-lines" style="background: rgba(15,10,8,0.5); border-left: 3px solid #444; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin: 2px 0; color: #b8b0a8;">
<div style="animation-delay:0.2s">Cleaning up dsFlower handles...</div>
<div style="animation-delay:0.6s">Logged out from BCN, MAD, LDN, BER, AMS</div>
</div>

</div>
</div>
