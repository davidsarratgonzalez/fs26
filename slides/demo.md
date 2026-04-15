<script setup>
import { ref, onMounted } from 'vue'

const terminal = ref(null)

onMounted(() => {
  if (!terminal.value) return
  const observer = new MutationObserver(() => {
    setTimeout(() => {
      terminal.value?.scrollTo({
        top: terminal.value.scrollHeight,
        behavior: 'smooth'
      })
    }, 50)
  })
  observer.observe(terminal.value, {
    childList: true, subtree: true,
    attributes: true, attributeFilter: ['class']
  })
})
</script>

## Live Demo

<div ref="terminal" style="overflow-y: auto; scroll-behavior: smooth; height: 430px; margin-top: 0.3em; scrollbar-width: none;">
<div style="font-size: 0.6em; line-height: 1.45; font-family: 'Roboto Mono', monospace;">

<!-- Login code (always visible) -->
<div style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; color: #c8b8a8;">
<span style="color:#78a9ff;">library</span>(<span style="color:#FFD000;">DSI</span>); <span style="color:#78a9ff;">library</span>(<span style="color:#FFD000;">DSOpal</span>); <span style="color:#78a9ff;">library</span>(<span style="color:#FFD000;">dsFlowerClient</span>)
<br/>
<br/>builder <span style="color:#888;">&lt;-</span> DSI::<span style="color:#78a9ff;">newDSLoginBuilder</span>()
<br/>builder$<span style="color:#78a9ff;">append</span>(server = <span style="color:#ffaacc;">"site1"</span>, url = <span style="color:#ffaacc;">"https://opal1.hospital-a.org"</span>,
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;table = <span style="color:#ffaacc;">"BRCA.diagnosis"</span>, driver = <span style="color:#ffaacc;">"OpalDriver"</span>) <span style="color:#666;"># credentials omitted</span>
<br/>builder$<span style="color:#78a9ff;">append</span>(server = <span style="color:#ffaacc;">"site2"</span>, url = <span style="color:#ffaacc;">"https://opal2.hospital-b.org"</span>, <span style="color:#666;">...</span>)
<br/>builder$<span style="color:#78a9ff;">append</span>(server = <span style="color:#ffaacc;">"site3"</span>, url = <span style="color:#ffaacc;">"https://opal3.hospital-c.org"</span>, <span style="color:#666;">...</span>)
<br/>
<br/>conns <span style="color:#888;">&lt;-</span> DSI::<span style="color:#78a9ff;">datashield.login</span>(logins = builder$<span style="color:#78a9ff;">build</span>(), assign = <span style="color:#88ccff;">TRUE</span>, symbol = <span style="color:#ffaacc;">"D"</span>)
</div>

<!-- Login output -->
<div v-click class="exec-lines" style="background: rgba(15,10,8,0.5); border-left: 3px solid #444; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin: 2px 0; color: #999;">
<div>Logging into the collaborating servers</div>
<div>&nbsp; Login site1: <span style="color:#66ddaa;">OK</span></div>
<div>&nbsp; Login site2: <span style="color:#66ddaa;">OK</span></div>
<div>&nbsp; Login site3: <span style="color:#66ddaa;">OK</span></div>
<div>Assigned table <span style="color:#c8b8a8;">BRCA.diagnosis</span> to symbol <span style="color:#c8b8a8;">"D"</span></div>
</div>

<!-- Connect -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
flower <span style="color:#888;">&lt;-</span> <span style="color:#78a9ff;">ds.flower.connect</span>(conns, symbol = <span style="color:#ffaacc;">"D"</span>)
</div>

<!-- Connect output -->
<div v-click class="exec-lines" style="background: rgba(15,10,8,0.5); border-left: 3px solid #444; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin: 2px 0; color: #999;">
<div>Initializing dsFlower on 3 servers...</div>
<div>&nbsp; site1: dsFlower v0.1.0 <span style="color:#888;">(847 rows x 12 cols)</span></div>
<div>&nbsp; site2: dsFlower v0.1.0 <span style="color:#888;">(623 rows x 12 cols)</span></div>
<div>&nbsp; site3: dsFlower v0.1.0 <span style="color:#888;">(531 rows x 12 cols)</span></div>
</div>

<!-- Recipe -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
recipe <span style="color:#888;">&lt;-</span> <span style="color:#78a9ff;">ds.flower.recipe</span>(
<br/>&nbsp;&nbsp;model &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;= ds.flower.model.<span style="color:#FFD000;">sklearn_logreg</span>(),
<br/>&nbsp;&nbsp;strategy &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;= ds.flower.strategy.<span style="color:#FFD000;">fedavg</span>(),
<br/>&nbsp;&nbsp;target_column = <span style="color:#ffaacc;">"diagnosis"</span>, num_rounds = <span style="color:#88ccff;">5L</span>)
</div>

<!-- Run -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
result <span style="color:#888;">&lt;-</span> <span style="color:#78a9ff;">ds.flower.run</span>(flower, recipe)
</div>

<!-- Run output -->
<div v-click class="exec-lines" style="background: rgba(15,10,8,0.5); border-left: 3px solid #444; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin: 2px 0; color: #999;">
<div>SuperLink started (PID: 26677, TLS)</div>
<div>&nbsp; site1: SuperNode <span style="color:#66ddaa;">connected</span></div>
<div>&nbsp; site2: SuperNode <span style="color:#66ddaa;">connected</span></div>
<div>&nbsp; site3: SuperNode <span style="color:#66ddaa;">connected</span></div>
<div>&nbsp; Code verification <span style="color:#66ddaa;">passed</span> on all servers</div>
<div><span style="color:#88ccff;">[ROUND 1/5]</span> 3 clients, loss: 0.6931</div>
<div><span style="color:#88ccff;">[ROUND 2/5]</span> 3 clients, loss: 0.4218</div>
<div><span style="color:#88ccff;">[ROUND 3/5]</span> 3 clients, loss: 0.3104</div>
<div><span style="color:#88ccff;">[ROUND 4/5]</span> 3 clients, loss: 0.2567</div>
<div><span style="color:#88ccff;">[ROUND 5/5]</span> 3 clients, loss: 0.2201</div>
<div><span style="color:#66ddaa;">Model saved: sklearn_logreg_FedAvg_5r</span></div>
<div>SuperLink stopped</div>
</div>

<!-- History -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
result$history
</div>

<div v-click class="exec-lines" style="background: rgba(15,10,8,0.5); border-left: 3px solid #444; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin: 2px 0; color: #999;">
<div>&nbsp; round &nbsp; loss &nbsp;&nbsp;&nbsp; n_clients</div>
<div>&nbsp;&nbsp;&nbsp; 1 &nbsp;&nbsp; 0.6931 &nbsp;&nbsp;&nbsp;&nbsp; 3</div>
<div>&nbsp;&nbsp;&nbsp; 2 &nbsp;&nbsp; 0.4218 &nbsp;&nbsp;&nbsp;&nbsp; 3</div>
<div>&nbsp;&nbsp;&nbsp; 3 &nbsp;&nbsp; 0.3104 &nbsp;&nbsp;&nbsp;&nbsp; 3</div>
<div>&nbsp;&nbsp;&nbsp; 4 &nbsp;&nbsp; 0.2567 &nbsp;&nbsp;&nbsp;&nbsp; 3</div>
<div>&nbsp;&nbsp;&nbsp; 5 &nbsp;&nbsp; 0.2201 &nbsp;&nbsp;&nbsp;&nbsp; 3</div>
</div>

<!-- Predict -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
preds <span style="color:#888;">&lt;-</span> <span style="color:#78a9ff;">ds.flower.predict</span>(result, newdata = test_data)
<br/><span style="color:#78a9ff;">table</span>(preds, test_data$diagnosis)
</div>

<div v-click class="exec-lines" style="background: rgba(15,10,8,0.5); border-left: 3px solid #444; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin: 2px 0; color: #999;">
<div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; benign &nbsp;malignant</div>
<div>&nbsp; benign &nbsp;&nbsp;&nbsp; 48 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 3</div>
<div>&nbsp; malignant &nbsp; 5 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;31</div>
</div>

<!-- Disconnect -->
<div v-click style="background: rgba(15,10,8,0.7); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
<span style="color:#78a9ff;">ds.flower.disconnect</span>(flower)
<br/>DSI::<span style="color:#78a9ff;">datashield.logout</span>(conns)
</div>

</div>
</div>
