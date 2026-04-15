## Live Demo

<div style="overflow: hidden; height: 420px; margin-top: 0.3em;">
<div style="font-size: 0.58em; line-height: 1.4; font-family: 'Roboto Mono', monospace;" v-motion :initial="{ y: 0 }" :click-6="{ y: -60 }" :click-7="{ y: -90 }" :click-8="{ y: -170 }" :click-9="{ y: -210 }" :click-10="{ y: -260 }" :click-11="{ y: -300 }">

<!-- Login code (always visible) -->
<div style="background: rgba(0,0,0,0.35); border-radius: 6px; padding: 0.5em 0.8em; color: #c8b8a8;">
<span style="color:#666;">></span> builder <span style="color:#888;">&lt;-</span> DSI::newDSLoginBuilder()
<br/><span style="color:#666;">></span> builder$append(server=<span style="color:#ffaacc;">"site1"</span>, url=<span style="color:#ffaacc;">"https://opal1.hospital-a.org"</span>, <span style="color:#888;">...</span>)
<br/><span style="color:#666;">></span> builder$append(server=<span style="color:#ffaacc;">"site2"</span>, url=<span style="color:#ffaacc;">"https://opal2.hospital-b.org"</span>, <span style="color:#888;">...</span>)
<br/><span style="color:#666;">></span> builder$append(server=<span style="color:#ffaacc;">"site3"</span>, url=<span style="color:#ffaacc;">"https://opal3.hospital-c.org"</span>, <span style="color:#888;">...</span>)
<br/><span style="color:#666;">></span> conns <span style="color:#888;">&lt;-</span> DSI::datashield.login(logins = builder$build(), assign = <span style="color:#88ccff;">TRUE</span>, symbol = <span style="color:#ffaacc;">"D"</span>)
</div>

<!-- Login output -->
<div v-click style="border-left: 3px solid #555; padding: 0.3em 0.7em; margin: 2px 0; color: #999;">
## Logging into the collaborating servers<br/>
## &nbsp; Login site1: OK &nbsp; Login site2: OK &nbsp; Login site3: OK<br/>
## Assigned table STUDY.data to symbol "D"
</div>

<!-- Connect -->
<div v-click style="background: rgba(0,0,0,0.35); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
<span style="color:#666;">></span> flower <span style="color:#888;">&lt;-</span> ds.flower.connect(conns, symbol = <span style="color:#ffaacc;">"D"</span>)
</div>

<!-- Connect output -->
<div v-click style="border-left: 3px solid #555; padding: 0.3em 0.7em; margin: 2px 0; color: #999;">
## &nbsp; site1: dsFlower v0.1.0 (847 rows x 12 cols)<br/>
## &nbsp; site2: dsFlower v0.1.0 (623 rows x 12 cols)<br/>
## &nbsp; site3: dsFlower v0.1.0 (531 rows x 12 cols)
</div>

<!-- Recipe -->
<div v-click style="background: rgba(0,0,0,0.35); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
<span style="color:#666;">></span> recipe <span style="color:#888;">&lt;-</span> ds.flower.recipe(
<br/>&nbsp;&nbsp;&nbsp; model &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;= ds.flower.model.<span style="color:#FFD000;">sklearn_logreg</span>(),
<br/>&nbsp;&nbsp;&nbsp; strategy &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;= ds.flower.strategy.<span style="color:#FFD000;">fedavg</span>(),
<br/>&nbsp;&nbsp;&nbsp; target_column = <span style="color:#ffaacc;">"diagnosis"</span>, num_rounds = <span style="color:#88ccff;">5L</span>)
</div>

<!-- Run -->
<div v-click style="background: rgba(0,0,0,0.35); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
<span style="color:#666;">></span> result <span style="color:#888;">&lt;-</span> ds.flower.run(flower, recipe)
</div>

<!-- Run output -->
<div v-click style="border-left: 3px solid #555; padding: 0.3em 0.7em; margin: 2px 0; color: #999;">
## SuperLink started (PID: 26677, TLS)<br/>
## &nbsp; site1: SuperNode connected<br/>
## &nbsp; site2: SuperNode connected<br/>
## &nbsp; site3: SuperNode connected<br/>
## &nbsp; Code verification passed on all servers<br/>
## <span style="color:#88ccff;">[ROUND 1]</span> 3 clients &mdash; loss: 0.6931<br/>
## <span style="color:#88ccff;">[ROUND 2]</span> 3 clients &mdash; loss: 0.4218<br/>
## <span style="color:#88ccff;">[ROUND 3]</span> 3 clients &mdash; loss: 0.3104<br/>
## <span style="color:#88ccff;">[ROUND 4]</span> 3 clients &mdash; loss: 0.2567<br/>
## <span style="color:#88ccff;">[ROUND 5]</span> 3 clients &mdash; loss: 0.2201<br/>
## <span style="color:#66ddaa;">Model saved: sklearn_logreg_FedAvg_5r</span>
</div>

<!-- History -->
<div v-click style="background: rgba(0,0,0,0.35); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
<span style="color:#666;">></span> result$history
</div>

<div v-click style="border-left: 3px solid #555; padding: 0.3em 0.7em; margin: 2px 0; color: #999;">
## &nbsp; round &nbsp; loss &nbsp;&nbsp;&nbsp; n_clients<br/>
## &nbsp;&nbsp;&nbsp; 1 &nbsp;&nbsp; 0.6931 &nbsp;&nbsp;&nbsp;&nbsp; 3<br/>
## &nbsp;&nbsp;&nbsp; 2 &nbsp;&nbsp; 0.4218 &nbsp;&nbsp;&nbsp;&nbsp; 3<br/>
## &nbsp;&nbsp;&nbsp; 3 &nbsp;&nbsp; 0.3104 &nbsp;&nbsp;&nbsp;&nbsp; 3<br/>
## &nbsp;&nbsp;&nbsp; 4 &nbsp;&nbsp; 0.2567 &nbsp;&nbsp;&nbsp;&nbsp; 3<br/>
## &nbsp;&nbsp;&nbsp; 5 &nbsp;&nbsp; 0.2201 &nbsp;&nbsp;&nbsp;&nbsp; 3
</div>

<!-- Weights -->
<div v-click style="background: rgba(0,0,0,0.35); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
<span style="color:#666;">></span> result$weights
</div>

<div v-click style="border-left: 3px solid #555; padding: 0.3em 0.7em; margin: 2px 0; color: #999;">
## $coef<br/>
## &nbsp; [1] &nbsp;0.4231 -0.1872 &nbsp;0.6543 -0.3218 &nbsp;0.5102 ...<br/>
## $intercept<br/>
## &nbsp; [1] -0.2341
</div>

<!-- Disconnect -->
<div v-click style="background: rgba(0,0,0,0.35); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 4px; color: #c8b8a8;">
<span style="color:#666;">></span> ds.flower.disconnect(flower)
<br/><span style="color:#666;">></span> DSI::datashield.logout(conns)
</div>

</div>
</div>
