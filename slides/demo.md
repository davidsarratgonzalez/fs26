## Live Demo

<div style="font-size: 0.62em; line-height: 1.45; overflow: hidden;">

<div style="font-family: 'Roboto Mono', monospace;">

<!-- Step 1: Login -->
<div style="background: rgba(0,0,0,0.3); border-radius: 6px; padding: 0.4em 0.7em; color: #c8b8a8;">
<span style="color:#888;">></span> builder <span style="color:#888;">&lt;-</span> DSI::newDSLoginBuilder()
<br/><span style="color:#888;">></span> builder$append(server=<span style="color:#ffaacc;">"hospital_a"</span>, url=<span style="color:#ffaacc;">"https://opal-a.org"</span>, table=<span style="color:#ffaacc;">"STUDY.data"</span>, <span style="color:#888;">...</span>)
<br/><span style="color:#888;">></span> builder$append(server=<span style="color:#ffaacc;">"hospital_b"</span>, url=<span style="color:#ffaacc;">"https://opal-b.org"</span>, table=<span style="color:#ffaacc;">"STUDY.data"</span>, <span style="color:#888;">...</span>)
<br/><span style="color:#888;">></span> builder$append(server=<span style="color:#ffaacc;">"hospital_c"</span>, url=<span style="color:#ffaacc;">"https://opal-c.org"</span>, table=<span style="color:#ffaacc;">"STUDY.data"</span>, <span style="color:#888;">...</span>)
<br/><span style="color:#888;">></span> conns <span style="color:#888;">&lt;-</span> DSI::datashield.login(logins = builder$build(), assign = <span style="color:#88ccff;">TRUE</span>, symbol = <span style="color:#ffaacc;">"D"</span>)
</div>

<!-- Step 1 output -->
<div v-click style="background: rgba(102,221,170,0.08); border-left: 3px solid #66ddaa; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin-top: 2px; color: #66ddaa;">
Logging into the collaborating servers<br/>
&nbsp; Login hospital_a: OK<br/>
&nbsp; Login hospital_b: OK<br/>
&nbsp; Login hospital_c: OK<br/>
Assigned table STUDY.data to symbol "D"
</div>

<!-- Step 2: Connect -->
<div v-click style="background: rgba(0,0,0,0.3); border-radius: 6px; padding: 0.4em 0.7em; margin-top: 6px; color: #c8b8a8;">
<span style="color:#888;">></span> flower <span style="color:#888;">&lt;-</span> ds.flower.connect(conns, symbol = <span style="color:#ffaacc;">"D"</span>)
</div>

<div v-click style="background: rgba(102,221,170,0.08); border-left: 3px solid #66ddaa; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin-top: 2px; color: #66ddaa;">
Initializing dsFlower on 3 servers...<br/>
&nbsp; hospital_a: dsFlower v0.1.0 &mdash; 847 rows x 12 cols<br/>
&nbsp; hospital_b: dsFlower v0.1.0 &mdash; 623 rows x 12 cols<br/>
&nbsp; hospital_c: dsFlower v0.1.0 &mdash; 531 rows x 12 cols
</div>

<!-- Step 3: Recipe -->
<div v-click style="background: rgba(0,0,0,0.3); border-radius: 6px; padding: 0.4em 0.7em; margin-top: 6px; color: #c8b8a8;">
<span style="color:#888;">></span> recipe <span style="color:#888;">&lt;-</span> ds.flower.recipe(
<br/>&nbsp;&nbsp;&nbsp; model &nbsp;&nbsp;&nbsp;&nbsp;= ds.flower.model.<span style="color:#FFD000;">sklearn_logreg</span>(),
<br/>&nbsp;&nbsp;&nbsp; strategy &nbsp;= ds.flower.strategy.<span style="color:#FFD000;">fedavg</span>(),
<br/>&nbsp;&nbsp;&nbsp; target_column = <span style="color:#ffaacc;">"diagnosis"</span>,
<br/>&nbsp;&nbsp;&nbsp; num_rounds &nbsp;&nbsp;&nbsp;= <span style="color:#88ccff;">5L</span>
<br/>)
</div>

<!-- Step 4: Run -->
<div v-click style="background: rgba(0,0,0,0.3); border-radius: 6px; padding: 0.4em 0.7em; margin-top: 6px; color: #c8b8a8;">
<span style="color:#888;">></span> result <span style="color:#888;">&lt;-</span> ds.flower.run(flower, recipe)
</div>

<div v-click style="background: rgba(102,221,170,0.08); border-left: 3px solid #66ddaa; border-radius: 0 6px 6px 0; padding: 0.3em 0.7em; margin-top: 2px; color: #66ddaa;">
&#9654; SuperLink started (TLS, port 9092)<br/>
&#9654; Preparing data on 3 servers... OK<br/>
&#9654; 3 SuperNodes connected<br/>
&#9654; Verifying app integrity (SHA-256)... OK<br/>
<span style="color:#88ccff;">Round 1/5</span> &mdash; loss: 0.6931 &nbsp;(3 clients, 0 failures)<br/>
<span style="color:#88ccff;">Round 2/5</span> &mdash; loss: 0.4218 &nbsp;(3 clients, 0 failures)<br/>
<span style="color:#88ccff;">Round 3/5</span> &mdash; loss: 0.3104 &nbsp;(3 clients, 0 failures)<br/>
<span style="color:#88ccff;">Round 4/5</span> &mdash; loss: 0.2567 &nbsp;(3 clients, 0 failures)<br/>
<span style="color:#88ccff;">Round 5/5</span> &mdash; loss: 0.2201 &nbsp;(3 clients, 0 failures)<br/>
&#9654; Global model saved: sklearn_logreg_FedAvg_5r<br/>
&#9654; SuperLink stopped
</div>

<!-- Step 5: Disconnect -->
<div v-click style="background: rgba(0,0,0,0.3); border-radius: 6px; padding: 0.4em 0.7em; margin-top: 6px; color: #c8b8a8;">
<span style="color:#888;">></span> ds.flower.disconnect(flower)
</div>

</div>
</div>
