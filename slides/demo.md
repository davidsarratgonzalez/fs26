<script setup>
import { ref, onMounted, onActivated, nextTick } from 'vue'
import { useSlideContext } from '@slidev/client'

const terminal = ref(null)
const slideCtx = useSlideContext()
let debounce = null

// Register global reset function for backward navigation
function resetDemo() {
  slideCtx.$clicks.value = 0
  nextTick(() => {
    if (terminal.value) {
      terminal.value.scrollTop = 0
      terminal.value.querySelectorAll('.exec-lines > div').forEach(el => {
        el.style.opacity = ''
        el.style.animation = ''
      })
    }
  })
}

onActivated(() => resetDemo())

// Expose reset via window so global-top can trigger it
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

## Live Demo

<div ref="terminal" style="overflow-y: auto; scroll-behavior: smooth; height: 430px; margin-top: 0.3em; scrollbar-width: none;">
<div style="font-size: 0.55em; line-height: 1.4; font-family: 'Roboto Mono', monospace;">

<!-- Experiment setup (always visible) -->
<div style="background: rgba(136,204,255,0.04); border: 1px solid rgba(136,204,255,0.12); border-radius: 8px; padding: 0.7em 1em; margin-bottom: 8px;">
<div style="color: #88ccff; font-size: 1.15em; font-weight: 500; margin-bottom: 8px;">Federated Tabular Classification</div>

<div style="display: flex; gap: 8px; margin-bottom: 8px;">
  <div style="flex:1; background: rgba(255,255,255,0.04); border: 1px solid rgba(255,255,255,0.08); border-radius: 6px; padding: 6px 8px;">
    <div style="color: #FFD000; font-weight: 500;">site1</div>
    <div style="color: #b0b8c0;">opal1.hospital-a.org</div>
    <div style="color: #999;">847 rows x 12 cols</div>
  </div>
  <div style="flex:1; background: rgba(255,255,255,0.04); border: 1px solid rgba(255,255,255,0.08); border-radius: 6px; padding: 6px 8px;">
    <div style="color: #FFD000; font-weight: 500;">site2</div>
    <div style="color: #b0b8c0;">opal2.hospital-b.org</div>
    <div style="color: #999;">623 rows x 12 cols</div>
  </div>
  <div style="flex:1; background: rgba(255,255,255,0.04); border: 1px solid rgba(255,255,255,0.08); border-radius: 6px; padding: 6px 8px;">
    <div style="color: #FFD000; font-weight: 500;">site3</div>
    <div style="color: #b0b8c0;">opal3.hospital-c.org</div>
    <div style="color: #999;">531 rows x 12 cols</div>
  </div>
</div>

<div style="color: #b0b8c0; line-height: 1.6; margin-bottom: 6px;">
<span style="color:#ffb366;">Table:</span> CLINICAL.breast_cancer &nbsp;&nbsp;
<span style="color:#ffb366;">Target:</span> <span style="background:rgba(102,221,170,0.1); border:1px solid rgba(102,221,170,0.2); border-radius:3px; padding:1px 6px; color:#66ddaa;">malignant</span> <span style="color:#888;">(binary)</span><br/>
<span style="color:#ffb366;">Features:</span>
<span style="background:rgba(255,208,0,0.08); border:1px solid rgba(255,208,0,0.12); border-radius:3px; padding:1px 5px; color:#FFD000; margin:1px; display:inline-block;">radius</span>
<span style="background:rgba(255,208,0,0.08); border:1px solid rgba(255,208,0,0.12); border-radius:3px; padding:1px 5px; color:#FFD000; margin:1px; display:inline-block;">texture</span>
<span style="background:rgba(255,208,0,0.08); border:1px solid rgba(255,208,0,0.12); border-radius:3px; padding:1px 5px; color:#FFD000; margin:1px; display:inline-block;">perimeter</span>
<span style="background:rgba(255,208,0,0.08); border:1px solid rgba(255,208,0,0.12); border-radius:3px; padding:1px 5px; color:#FFD000; margin:1px; display:inline-block;">area</span>
<span style="background:rgba(255,208,0,0.08); border:1px solid rgba(255,208,0,0.12); border-radius:3px; padding:1px 5px; color:#FFD000; margin:1px; display:inline-block;">smoothness</span>
<span style="background:rgba(255,208,0,0.08); border:1px solid rgba(255,208,0,0.12); border-radius:3px; padding:1px 5px; color:#FFD000; margin:1px; display:inline-block;">compactness</span>
<span style="background:rgba(255,208,0,0.08); border:1px solid rgba(255,208,0,0.12); border-radius:3px; padding:1px 5px; color:#FFD000; margin:1px; display:inline-block;">concavity</span>
<span style="background:rgba(255,208,0,0.08); border:1px solid rgba(255,208,0,0.12); border-radius:3px; padding:1px 5px; color:#FFD000; margin:1px; display:inline-block;">symmetry</span>
<span style="color:#888; margin-left:2px;">+4 more</span>
</div>

<div style="color: #b0b8c0; line-height: 1.5;">
<span style="color:#88ccff;">Plan:</span><br/>
<span style="color:#999;">&nbsp; 1.</span> <span style="color:#e0d8d0;">sklearn LogReg</span> <span style="color:#888;">(FedAvg)</span><br/>
<span style="color:#999;">&nbsp; 2.</span> <span style="color:#e0d8d0;">PyTorch MLP</span> <span style="color:#888;">(FedProx, hidden: 32,16)</span><br/>
<span style="color:#999;">&nbsp; 3.</span> <span style="color:#e0d8d0;">Compare final losses</span>
</div>
</div>

<!-- Libraries (first click) -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; color: #c8b8a8;">
<span style="color:#78a9ff;">library</span>(<span style="color:#FFD000;">DSI</span>)
<br/><span style="color:#78a9ff;">library</span>(<span style="color:#FFD000;">DSOpal</span>)
<br/><span style="color:#78a9ff;">library</span>(<span style="color:#FFD000;">dsFlowerClient</span>)
</div>

<!-- Login -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
builder <span style="color:#888;">&lt;-</span> DSI::<span style="color:#78a9ff;">newDSLoginBuilder</span>()
<br/><span style="color:#78a9ff;">for</span> (i <span style="color:#78a9ff;">in</span> <span style="color:#88ccff;">1</span>:<span style="color:#88ccff;">3</span>) {
<br/>&nbsp;&nbsp;builder$<span style="color:#78a9ff;">append</span>(
<br/>&nbsp;&nbsp;&nbsp;&nbsp;server &nbsp;= <span style="color:#78a9ff;">paste0</span>(<span style="color:#ffaacc;">"site"</span>, i),
<br/>&nbsp;&nbsp;&nbsp;&nbsp;url &nbsp;&nbsp;&nbsp;&nbsp;= <span style="color:#78a9ff;">paste0</span>(<span style="color:#ffaacc;">"https://opal"</span>, i, <span style="color:#ffaacc;">":8443"</span>),
<br/>&nbsp;&nbsp;&nbsp;&nbsp;table &nbsp;&nbsp;= <span style="color:#ffaacc;">"CLINICAL.breast_cancer"</span>,
<br/>&nbsp;&nbsp;&nbsp;&nbsp;driver &nbsp;= <span style="color:#ffaacc;">"OpalDriver"</span>, <span style="color:#666;">...</span> <span style="color:#666;"># credentials omitted</span>
<br/>&nbsp;&nbsp;)
<br/>}
<br/>conns <span style="color:#888;">&lt;-</span> DSI::<span style="color:#78a9ff;">datashield.login</span>(logins = builder$<span style="color:#78a9ff;">build</span>(), assign = <span style="color:#88ccff;">TRUE</span>, symbol = <span style="color:#ffaacc;">"D"</span>)
</div>

<div v-click class="exec-lines" style="background: rgba(15,10,8,0.5); border-left: 3px solid #444; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin: 2px 0; color: #999;">
<div>Logging into the collaborating servers</div>
<div>&nbsp; Login site1: <span style="color:#66ddaa;">OK</span></div>
<div>&nbsp; Login site2: <span style="color:#66ddaa;">OK</span></div>
<div>&nbsp; Login site3: <span style="color:#66ddaa;">OK</span></div>
<div>Assigned table CLINICAL.breast_cancer to symbol "D"</div>
</div>

<!-- Connect -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
flower <span style="color:#888;">&lt;-</span> <span style="color:#78a9ff;">ds.flower.connect</span>(conns, symbol = <span style="color:#ffaacc;">"D"</span>)
</div>

<!-- Describe -->
<div v-click class="exec-lines" style="background: rgba(15,10,8,0.5); border-left: 3px solid #444; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin: 2px 0; color: #999;">
<div>&nbsp; site1: dsFlower v0.1.0 <span style="color:#888;">(847 rows x 12 cols)</span></div>
<div>&nbsp; site2: dsFlower v0.1.0 <span style="color:#888;">(623 rows x 12 cols)</span></div>
<div>&nbsp; site3: dsFlower v0.1.0 <span style="color:#888;">(531 rows x 12 cols)</span></div>
<div>&nbsp; Available templates: sklearn_logreg, pytorch_mlp, pytorch_resnet18, xgboost, <span style="color:#888;">...</span></div>
<div>&nbsp; Trust profile: <span style="color:#66ddaa;">clinical_default</span> (SecAgg+ required)</div>
</div>

<!-- Run 1: LogReg -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
recipe_logreg <span style="color:#888;">&lt;-</span> <span style="color:#78a9ff;">ds.flower.recipe</span>(
<br/>&nbsp;&nbsp;model &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;= ds.flower.model.<span style="color:#FFD000;">sklearn_logreg</span>(C = <span style="color:#88ccff;">1.0</span>, max_iter = <span style="color:#88ccff;">200L</span>),
<br/>&nbsp;&nbsp;target_column = <span style="color:#ffaacc;">"malignant"</span>,
<br/>&nbsp;&nbsp;num_rounds &nbsp;&nbsp;&nbsp;= <span style="color:#88ccff;">5L</span>
<br/>)
<br/>result_logreg <span style="color:#888;">&lt;-</span> <span style="color:#78a9ff;">ds.flower.run</span>(flower, recipe_logreg)
</div>

<div v-click class="exec-lines" style="background: rgba(15,10,8,0.5); border-left: 3px solid #444; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin: 2px 0; color: #999;">
<div>SuperLink started (PID: 26677)</div>
<div>&nbsp; Fleet API (SuperNodes): 127.0.0.1:9092</div>
<div>&nbsp; site1: SuperLink reachable at host.docker.internal:9092</div>
<div>&nbsp; site2: SuperLink reachable at host.docker.internal:9092</div>
<div>&nbsp; site3: SuperLink reachable at host.docker.internal:9092</div>
<div>&nbsp; site1: SuperNode <span style="color:#66ddaa;">connected</span></div>
<div>&nbsp; site2: SuperNode <span style="color:#66ddaa;">connected</span></div>
<div>&nbsp; site3: SuperNode <span style="color:#66ddaa;">connected</span></div>
<div>&nbsp; Code verification <span style="color:#66ddaa;">passed</span> on all servers</div>
<div><span style="color:#88ccff;">[ROUND 1/5]</span> sampled 3 clients &mdash; received 3 results, 0 failures</div>
<div><span style="color:#88ccff;">[ROUND 2/5]</span> sampled 3 clients &mdash; received 3 results, 0 failures</div>
<div><span style="color:#88ccff;">[ROUND 3/5]</span> sampled 3 clients &mdash; received 3 results, 0 failures</div>
<div><span style="color:#88ccff;">[ROUND 4/5]</span> sampled 3 clients &mdash; received 3 results, 0 failures</div>
<div><span style="color:#88ccff;">[ROUND 5/5]</span> sampled 3 clients &mdash; received 3 results, 0 failures</div>
<div><span style="color:#66ddaa;">Model saved to ./dsflower_output/sklearn_logreg_FedAvg_5r_20260325_223015</span></div>
<div>SuperLink stopped.</div>
</div>

<!-- Final loss 1 -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
<span style="color:#78a9ff;">cat</span>(<span style="color:#ffaacc;">"Final loss:"</span>, <span style="color:#78a9ff;">tail</span>(result_logreg$history$loss, <span style="color:#88ccff;">1</span>), <span style="color:#ffaacc;">"\n"</span>)
</div>

<div v-click class="exec-lines" style="background: rgba(15,10,8,0.5); border-left: 3px solid #444; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin: 2px 0; color: #999;">
<div>Final loss: <span style="color:#FFD000;">0.6095233</span></div>
</div>

<!-- Run 2: MLP + FedProx -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
recipe_mlp <span style="color:#888;">&lt;-</span> <span style="color:#78a9ff;">ds.flower.recipe</span>(
<br/>&nbsp;&nbsp;model &nbsp;&nbsp;&nbsp;&nbsp;= ds.flower.model.<span style="color:#FFD000;">pytorch_mlp</span>(hidden_layers = <span style="color:#ffaacc;">"32,16"</span>,
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;learning_rate = <span style="color:#88ccff;">0.01</span>,
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;batch_size = <span style="color:#88ccff;">32L</span>,
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;local_epochs = <span style="color:#88ccff;">2L</span>),
<br/>&nbsp;&nbsp;strategy &nbsp;= ds.flower.strategy.<span style="color:#FFD000;">fedprox</span>(proximal_mu = <span style="color:#88ccff;">0.1</span>),
<br/>&nbsp;&nbsp;target_column = <span style="color:#ffaacc;">"malignant"</span>,
<br/>&nbsp;&nbsp;num_rounds &nbsp;&nbsp;&nbsp;= <span style="color:#88ccff;">5L</span>
<br/>)
<br/>result_mlp <span style="color:#888;">&lt;-</span> <span style="color:#78a9ff;">ds.flower.run</span>(flower, recipe_mlp)
</div>

<div v-click class="exec-lines" style="background: rgba(15,10,8,0.5); border-left: 3px solid #444; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin: 2px 0; color: #999;">
<div>SuperLink started (PID: 29346)</div>
<div>&nbsp; Fleet API (SuperNodes): 127.0.0.1:9092</div>
<div>&nbsp; site1: SuperLink reachable at host.docker.internal:9092</div>
<div>&nbsp; site2: SuperLink reachable at host.docker.internal:9092</div>
<div>&nbsp; site3: SuperLink reachable at host.docker.internal:9092</div>
<div>&nbsp; site1: SuperNode <span style="color:#66ddaa;">connected</span></div>
<div>&nbsp; site2: SuperNode <span style="color:#66ddaa;">connected</span></div>
<div>&nbsp; site3: SuperNode <span style="color:#66ddaa;">connected</span></div>
<div>&nbsp; Code verification <span style="color:#66ddaa;">passed</span> on all servers</div>
<div><span style="color:#88ccff;">[ROUND 1/5]</span> sampled 3 clients &mdash; received 3 results, 0 failures</div>
<div><span style="color:#88ccff;">[ROUND 2/5]</span> sampled 3 clients &mdash; received 3 results, 0 failures</div>
<div><span style="color:#88ccff;">[ROUND 3/5]</span> sampled 3 clients &mdash; received 3 results, 0 failures</div>
<div><span style="color:#88ccff;">[ROUND 4/5]</span> sampled 3 clients &mdash; received 3 results, 0 failures</div>
<div><span style="color:#88ccff;">[ROUND 5/5]</span> sampled 3 clients &mdash; received 3 results, 0 failures</div>
<div><span style="color:#66ddaa;">Model saved to ./dsflower_output/pytorch_mlp_FedProx_5r_20260325_223934</span></div>
<div>SuperLink stopped.</div>
</div>

<!-- Final loss 2 -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
<span style="color:#78a9ff;">cat</span>(<span style="color:#ffaacc;">"Final loss:"</span>, <span style="color:#78a9ff;">tail</span>(result_mlp$history$loss, <span style="color:#88ccff;">1</span>), <span style="color:#ffaacc;">"\n"</span>)
</div>

<div v-click class="exec-lines" style="background: rgba(15,10,8,0.5); border-left: 3px solid #444; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin: 2px 0; color: #999;">
<div>Final loss: <span style="color:#FFD000;">0.6473228</span></div>
</div>

<!-- Comparison -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
results <span style="color:#888;">&lt;-</span> <span style="color:#78a9ff;">data.frame</span>(
<br/>&nbsp;&nbsp;model &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;= <span style="color:#78a9ff;">c</span>(<span style="color:#ffaacc;">"sklearn_logreg"</span>, <span style="color:#ffaacc;">"pytorch_mlp"</span>),
<br/>&nbsp;&nbsp;final_loss = <span style="color:#78a9ff;">c</span>(
<br/>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#78a9ff;">tail</span>(result_logreg$history$loss, <span style="color:#88ccff;">1</span>),
<br/>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#78a9ff;">tail</span>(result_mlp$history$loss, <span style="color:#88ccff;">1</span>))
<br/>)
<br/><span style="color:#78a9ff;">print</span>(results)
</div>

<div v-click class="exec-lines" style="background: rgba(15,10,8,0.5); border-left: 3px solid #444; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin: 2px 0; color: #999;">
<div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model final_loss</div>
<div>&nbsp; 1 sklearn_logreg &nbsp;<span style="color:#FFD000;">0.6095233</span></div>
<div>&nbsp; 2 &nbsp;&nbsp;&nbsp;pytorch_mlp &nbsp;<span style="color:#FFD000;">0.6473228</span></div>
</div>

<!-- Predict -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
preds <span style="color:#888;">&lt;-</span> <span style="color:#78a9ff;">ds.flower.predict</span>(result_logreg, newdata = test_data)
<br/><span style="color:#78a9ff;">table</span>(preds, test_data$malignant)
</div>

<div v-click class="exec-lines" style="background: rgba(15,10,8,0.5); border-left: 3px solid #444; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin: 2px 0; color: #999;">
<div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 0 &nbsp;&nbsp;1</div>
<div>&nbsp; benign &nbsp;48 &nbsp;&nbsp;3</div>
<div>&nbsp; malign &nbsp;&nbsp;5 &nbsp;31</div>
</div>

<!-- Disconnect -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
<span style="color:#78a9ff;">ds.flower.disconnect</span>(flower)
<br/><span style="color:#78a9ff;">datashield.logout</span>(conns)
</div>

</div>
</div>
