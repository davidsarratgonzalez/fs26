## Live Demo

<div style="font-size: 0.72em; line-height: 1.5;">

```r
# 1. Login to 3 hospital Opal servers
builder <- DSI::newDSLoginBuilder()
builder$append(server="hospital_a", url="https://opal-a.org", table="STUDY.data", ...)
builder$append(server="hospital_b", url="https://opal-b.org", table="STUDY.data", ...)
builder$append(server="hospital_c", url="https://opal-c.org", table="STUDY.data", ...)
conns <- DSI::datashield.login(logins = builder$build(), assign = TRUE, symbol = "D")
```

<div v-click style="margin-top:-0.5em;">

```r
# 2. Initialize dsFlower federation
flower <- ds.flower.connect(conns, symbol = "D")
```

</div>

<div v-click style="margin-top:-0.5em;">

```r
# 3. Compose a recipe
recipe <- ds.flower.recipe(
  model         = ds.flower.model.sklearn_logreg(),
  strategy      = ds.flower.strategy.fedavg(),
  target_column = "diagnosis",
  num_rounds    = 5L
)
```

</div>

<div v-click style="margin-top:-0.5em;">

```r
# 4. Run federated training (auto-manages SuperLink + SuperNodes)
result <- ds.flower.run(flower, recipe)
```

<div style="background: rgba(0,0,0,0.3); border-radius: 6px; padding: 0.5em 0.8em; margin-top: 0.3em; font-family: 'Roboto Mono', monospace; font-size: 0.85em; color: #66ddaa;">
&#9654; SuperLink started (TLS, port 9092)<br/>
&#9654; 3 SuperNodes connected<br/>
&#9654; Round 1/5 &mdash; loss: 0.6931 (3 clients)<br/>
&#9654; Round 2/5 &mdash; loss: 0.4218 (3 clients)<br/>
&#9654; Round 3/5 &mdash; loss: 0.3104 (3 clients)<br/>
&#9654; Round 4/5 &mdash; loss: 0.2567 (3 clients)<br/>
&#9654; Round 5/5 &mdash; loss: 0.2201 (3 clients)<br/>
&#9654; Global model saved &mdash; sklearn_logreg_FedAvg_5r
</div>

</div>

<div v-click style="margin-top:0.3em;">

```r
# 5. Done. Disconnect.
ds.flower.disconnect(flower)
```

</div>

</div>
