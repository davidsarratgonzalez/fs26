<script setup>
import { ref, onMounted, onActivated } from 'vue'

const terminal = ref(null)
let debounce = null

onActivated(() => {
  if (!terminal.value) return
  terminal.value.querySelectorAll('.exec-lines > div').forEach(el => {
    el.style.opacity = '1'
    el.style.animation = 'none'
  })
  terminal.value.scrollTop = terminal.value.scrollHeight
})

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
<div style="font-size: 0.58em; line-height: 1.4; font-family: 'Roboto Mono', monospace;">

<!-- Libraries + Login -->
<div style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; color: #c8b8a8;">
<span style="color:#78a9ff;">library</span>(<span style="color:#FFD000;">DSI</span>); <span style="color:#78a9ff;">library</span>(<span style="color:#FFD000;">DSOpal</span>); <span style="color:#78a9ff;">library</span>(<span style="color:#FFD000;">dsFlowerClient</span>)
<br/>
<br/>builder <span style="color:#888;">&lt;-</span> DSI::<span style="color:#78a9ff;">newDSLoginBuilder</span>()
<br/><span style="color:#78a9ff;">for</span> (i <span style="color:#78a9ff;">in</span> <span style="color:#88ccff;">1</span>:<span style="color:#88ccff;">3</span>) builder$<span style="color:#78a9ff;">append</span>(
<br/>&nbsp;&nbsp;server = <span style="color:#78a9ff;">paste0</span>(<span style="color:#ffaacc;">"site"</span>, i), url = <span style="color:#78a9ff;">paste0</span>(<span style="color:#ffaacc;">"https://opal"</span>, i, <span style="color:#ffaacc;">":8443"</span>),
<br/>&nbsp;&nbsp;table = <span style="color:#ffaacc;">"CLINICAL.breast_cancer"</span>, driver = <span style="color:#ffaacc;">"OpalDriver"</span>, <span style="color:#666;">...</span>)
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

<!-- Run 1: LogReg -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
recipe_logreg <span style="color:#888;">&lt;-</span> <span style="color:#78a9ff;">ds.flower.recipe</span>(
<br/>&nbsp;&nbsp;model &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;= ds.flower.model.<span style="color:#FFD000;">sklearn_logreg</span>(C = <span style="color:#88ccff;">1.0</span>, max_iter = <span style="color:#88ccff;">200L</span>),
<br/>&nbsp;&nbsp;target_column = <span style="color:#ffaacc;">"malignant"</span>,
<br/>&nbsp;&nbsp;num_rounds &nbsp;&nbsp;&nbsp;= <span style="color:#88ccff;">5L</span>)
<br/>result_logreg <span style="color:#888;">&lt;-</span> <span style="color:#78a9ff;">ds.flower.run</span>(flower, recipe_logreg)
</div>

<div v-click class="exec-lines" style="background: rgba(15,10,8,0.5); border-left: 3px solid #444; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin: 2px 0; color: #999;">
<div>SuperLink started (PID: 26677)</div>
<div>&nbsp; site1: SuperNode <span style="color:#66ddaa;">connected</span></div>
<div>&nbsp; site2: SuperNode <span style="color:#66ddaa;">connected</span></div>
<div>&nbsp; site3: SuperNode <span style="color:#66ddaa;">connected</span></div>
<div>&nbsp; Code verification <span style="color:#66ddaa;">passed</span> on all servers</div>
<div><span style="color:#88ccff;">[ROUND 1/5]</span> 3 clients, 0 failures</div>
<div><span style="color:#88ccff;">[ROUND 2/5]</span> 3 clients, 0 failures</div>
<div><span style="color:#88ccff;">[ROUND 3/5]</span> 3 clients, 0 failures</div>
<div><span style="color:#88ccff;">[ROUND 4/5]</span> 3 clients, 0 failures</div>
<div><span style="color:#88ccff;">[ROUND 5/5]</span> 3 clients, 0 failures</div>
<div><span style="color:#66ddaa;">Model saved to ./dsflower_output/sklearn_logreg_FedAvg_5r</span></div>
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
<br/>&nbsp;&nbsp;model &nbsp;&nbsp;&nbsp;&nbsp;= ds.flower.model.<span style="color:#FFD000;">pytorch_mlp</span>(hidden_layers = <span style="color:#ffaacc;">"32,16"</span>, learning_rate = <span style="color:#88ccff;">0.01</span>),
<br/>&nbsp;&nbsp;strategy &nbsp;= ds.flower.strategy.<span style="color:#FFD000;">fedprox</span>(proximal_mu = <span style="color:#88ccff;">0.1</span>),
<br/>&nbsp;&nbsp;target_column = <span style="color:#ffaacc;">"malignant"</span>, num_rounds = <span style="color:#88ccff;">5L</span>)
<br/>result_mlp <span style="color:#888;">&lt;-</span> <span style="color:#78a9ff;">ds.flower.run</span>(flower, recipe_mlp)
</div>

<div v-click class="exec-lines" style="background: rgba(15,10,8,0.5); border-left: 3px solid #444; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin: 2px 0; color: #999;">
<div>SuperLink started (PID: 29346)</div>
<div>&nbsp; 3 SuperNodes <span style="color:#66ddaa;">connected</span> &mdash; Code verification <span style="color:#66ddaa;">passed</span></div>
<div><span style="color:#88ccff;">[ROUND 1-5/5]</span> 3 clients, 0 failures each round</div>
<div><span style="color:#66ddaa;">Model saved to ./dsflower_output/pytorch_mlp_FedProx_5r</span></div>
<div>Final loss: <span style="color:#FFD000;">0.6473228</span></div>
</div>

<!-- Comparison table -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
results <span style="color:#888;">&lt;-</span> <span style="color:#78a9ff;">data.frame</span>(model = <span style="color:#78a9ff;">c</span>(<span style="color:#ffaacc;">"sklearn_logreg"</span>, <span style="color:#ffaacc;">"pytorch_mlp"</span>),
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;final_loss = <span style="color:#78a9ff;">c</span>(<span style="color:#88ccff;">0.6095</span>, <span style="color:#88ccff;">0.6473</span>))
<br/><span style="color:#78a9ff;">print</span>(results)
</div>

<div v-click class="exec-lines" style="background: rgba(15,10,8,0.5); border-left: 3px solid #444; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin: 2px 0; color: #999;">
<div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model &nbsp;final_loss</div>
<div>&nbsp; 1 sklearn_logreg &nbsp;<span style="color:#FFD000;">0.6095</span></div>
<div>&nbsp; 2 &nbsp;&nbsp;&nbsp;pytorch_mlp &nbsp;<span style="color:#FFD000;">0.6473</span></div>
</div>

<!-- Disconnect -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
<span style="color:#78a9ff;">ds.flower.disconnect</span>(flower)
<br/>DSI::<span style="color:#78a9ff;">datashield.logout</span>(conns)
</div>

</div>
</div>
