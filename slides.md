---
theme: default
title: dsFlower
info: Federated Learning for DataSHIELD
class: text-center
drawings:
  persist: false
transition: fade
css: unocss
---

<style>
.hero-title {
  font-family: 'Roboto Mono', monospace;
  font-weight: 300;
  font-size: 4em;
  text-transform: uppercase;
  color: #10a34a;
  letter-spacing: 0.02em;
}
.hero-sub {
  font-family: 'Inter', sans-serif;
  font-weight: 300;
  font-size: 1.4em;
  color: #ababab;
  margin-top: 0.5em;
}
.hero-authors {
  font-family: 'Roboto Mono', monospace;
  font-size: 0.85em;
  color: #666;
  margin-top: 2em;
}
</style>

<div class="flex flex-col items-center justify-center h-full">
  <div class="hero-title">dsFlower</div>
  <div class="hero-sub">Federated Learning for DataSHIELD</div>
  <div class="hero-sub" style="font-size: 1em; color: #666; margin-top: 0.5em;">
    Powered by <a href="https://flower.ai" style="color: #10a34a;">Flower</a>
  </div>
  <div class="hero-authors">
    David Sarrat Gonz&aacute;lez &nbsp;&middot;&nbsp; Juan R Gonz&aacute;lez<br/>
    <span style="color: #444;">Barcelona Institute for Global Health (ISGlobal)</span>
  </div>
</div>

---

## The problem

Hospitals want to train ML models together **without sharing patient data**.

<div class="grid grid-cols-2 gap-8 mt-8">
<div>

### Without federation

- Pool all data in one place
- Privacy regulations block this
- Legal, ethical, and technical barriers
- Data stays siloed

</div>
<div>

### With dsFlower

- Data **never leaves** the hospital
- Only model weight updates travel
- Each site trains locally
- Coordinated by a central aggregator

</div>
</div>

---

## Architecture

<div class="text-center mt-4">

```
  Researcher (R)                     Hospital A (Rock)
  +------------------+               +----------------------+
  | dsFlowerClient   |  DataSHIELD   | dsFlower             |
  |   ds.flower.*()  |-------------->|   flowerInitDS()     |
  |                  |               |   flowerPrepareDS()  |
  | SuperLink        |   gRPC/TLS   |   SuperNode          |
  |   (localhost)    |<=============>|   (Flower ClientApp) |
  +------------------+    weights    +----------------------+
          |
          |              Hospital B (Rock)
          |              +----------------------+
          +==============>  SuperNode            |
                 gRPC    |  (Flower ClientApp)  |
                         +----------------------+
```

</div>

<div class="mt-4 text-center" style="color: #ababab; font-size: 0.9em;">
  DataSHIELD handles orchestration. <strong>Flower</strong> handles weight transport via gRPC.
  <br/>Raw data stays on each hospital's server.
</div>

---

## How it works

<div class="grid grid-cols-3 gap-6 mt-6">

<div class="text-center p-4" style="background: #111; border-radius: 8px; border: 1px solid #222;">
  <div style="font-size: 2em;">1</div>
  <div style="color: #10a34a; font-family: 'Roboto Mono', monospace; font-size: 0.9em;">CONNECT</div>
  <div style="font-size: 0.85em; color: #999; margin-top: 0.5em;">
    Researcher connects to N hospital nodes via DataSHIELD
  </div>
</div>

<div class="text-center p-4" style="background: #111; border-radius: 8px; border: 1px solid #222;">
  <div style="font-size: 2em;">2</div>
  <div style="color: #10a34a; font-family: 'Roboto Mono', monospace; font-size: 0.9em;">TRAIN</div>
  <div style="font-size: 0.85em; color: #999; margin-top: 0.5em;">
    Each node trains on local data, sends weight updates to SuperLink
  </div>
</div>

<div class="text-center p-4" style="background: #111; border-radius: 8px; border: 1px solid #222;">
  <div style="font-size: 2em;">3</div>
  <div style="color: #10a34a; font-family: 'Roboto Mono', monospace; font-size: 0.9em;">AGGREGATE</div>
  <div style="font-size: 0.85em; color: #999; margin-top: 0.5em;">
    SuperLink averages updates, sends global model back. Repeat N rounds.
  </div>
</div>

</div>

---

## Researcher API

```r
library(dsFlowerClient)

# Connect to 3 hospitals
conns <- DSI::datashield.login(logins = builder$build(),
                               assign = TRUE, symbol = "D")
flower <- ds.flower.connect(conns, symbol = "D")

# Define what to train
recipe <- ds.flower.recipe(
  model         = ds.flower.model.sklearn_logreg(),
  strategy      = ds.flower.strategy.fedavg(),
  target_column = "diagnosis",
  num_rounds    = 10L
)

# Train across all hospitals
result <- ds.flower.run(flower, recipe)
```

<div style="color: #666; font-size: 0.8em; margin-top: 0.5em;">
  One function call. All orchestration is automatic.
</div>

---

## Models

<div class="grid grid-cols-2 gap-6 mt-4">

<div>

| Framework | Templates |
|---|---|
| **scikit-learn** | LogReg, Ridge, SGD, Elastic Net, SVM |
| **PyTorch** | MLP, LogReg, Linear, Multiclass, Multilabel, Poisson |
| **PyTorch (survival)** | Cox PH, Log-Normal AFT, Cause-Specific Cox |
| **PyTorch (vision)** | ResNet-18, DenseNet-121, U-Net 2D |
| **PyTorch (sequence)** | LSTM, TCN |
| **XGBoost** | Secure histogram aggregation |

</div>

<div>

### 20 templates

Each template includes:
- `client_app.py` (training loop)
- `server_app.py` (aggregation)
- `task.py` (data loading)
- `privacy_utils.py` (DP, clipping)

The researcher picks a model.
The server does the rest.

</div>
</div>

---

## Strategies

<div class="mt-6">

| Strategy | Description | When to use |
|---|---|---|
| **FedAvg** | Standard averaging | Default, works well for IID data |
| **FedProx** | Proximal penalty term | Non-IID data across hospitals |
| **FedAdam** | Server-side Adam optimizer | Unstable convergence |
| **FedAdagrad** | Server-side Adagrad | Sparse features |
| **FedBN** | Excludes BatchNorm from aggregation | Different scanners/protocols per site |

</div>

<div class="mt-6" style="color: #ababab; font-size: 0.9em;">

```r
recipe <- ds.flower.recipe(
  model    = ds.flower.model.pytorch_resnet18(),
  strategy = ds.flower.strategy.fedbn(),  # different scanners per hospital
  ...
)
```

</div>

---

## Privacy model

<div class="mt-4">

Four layers of protection against an untrusted researcher:

</div>

<div class="grid grid-cols-2 gap-6 mt-4">

<div>

### Layer 1 &mdash; DataSHIELD
Raw data stays on the server. The researcher only calls approved methods.

### Layer 2 &mdash; SecAgg+
Individual weight updates are encrypted. The researcher only sees the **aggregate**.

</div>
<div>

### Layer 3 &mdash; DP-SGD
Each node adds calibrated noise before sending updates. Formal privacy guarantees (Opacus).

### Layer 4 &mdash; Disclosure control
Bucketed counts, suppressed per-node metrics, minimum sample sizes, class balance checks.

</div>
</div>

---

## Privacy profiles

<div class="mt-4">

| Profile | SecAgg | DP | Min rows | Per-node metrics | Use case |
|---|---|---|---|---|---|
| `sandbox_open` | | | 3 | yes | Development |
| `trusted_internal` | | | 50 | yes | Single institution |
| `consortium_internal` | yes | | 50 | no | Multi-site consortium |
| `clinical_default` | yes | | 100 | no | Hospital deployment |
| `clinical_hardened` | yes | | 200 | no | High security |
| `clinical_update_noise` | yes | clipping + noise | 200 | no | Update-level DP |
| `high_sensitivity_dp` | yes | DP-SGD (Opacus) | 500 | no | Patient-level DP |

</div>

<div style="color: #666; font-size: 0.8em; margin-top: 0.5em;">
  Profiles are <strong>server-enforced</strong>. The researcher cannot bypass them.
</div>

---

## Demo: 3 hospitals, 3 algorithms

<div class="mt-4">

```r
# Connect to 3 Opal nodes
conns <- datashield.login(builder$build(), assign = TRUE, symbol = "D")
flower <- ds.flower.connect(conns, symbol = "D")

# 1. Logistic Regression (scikit-learn)
r1 <- ds.flower.run(flower, ds.flower.recipe(
  model = ds.flower.model.sklearn_logreg(), target_column = "malignant", num_rounds = 5L))

# 2. MLP with FedProx (PyTorch)
r2 <- ds.flower.run(flower, ds.flower.recipe(
  model = ds.flower.model.pytorch_mlp(hidden_layers = "32,16"),
  strategy = ds.flower.strategy.fedprox(proximal_mu = 0.1),
  target_column = "malignant", num_rounds = 5L))

# 3. XGBoost (secure histogram)
r3 <- ds.flower.run(flower, ds.flower.recipe(
  model = ds.flower.model.xgboost(max_depth = 4L),
  target_column = "malignant", num_rounds = 5L))
```

</div>

---

## Packages

<div class="grid grid-cols-2 gap-8 mt-6">
<div>

### Server-side (on each hospital)

| Package | Role |
|---|---|
| **dsFlower** | FL orchestration, privacy policy |
| **dsImaging** | Medical image datasets (S3/MinIO) |
| **dsRadiomics** | Feature extraction, segmentation |
| **dsJobs** | Durable job runtime |

</div>
<div>

### Client-side (researcher)

| Package | Role |
|---|---|
| **dsFlowerClient** | Recipe builder, training API |
| **dsImagingClient** | Dataset discovery |
| **dsRadiomicsClient** | Extraction workflows |
| **dsJobsClient** | Job monitoring |

</div>
</div>

<div class="mt-4" style="color: #666; font-size: 0.85em;">
  Client packages are lightweight (no arrow, no aws.s3, no DBI). All heavy dependencies stay server-side.
</div>

---

<div class="flex flex-col items-center justify-center h-full">
  <div style="font-family: 'Roboto Mono', monospace; font-weight: 300; font-size: 3em; text-transform: uppercase; color: #10a34a;">
    dsFlower
  </div>
  <div style="font-size: 1.2em; color: #ababab; margin-top: 0.5em;">
    github.com/isglobal-brge/dsFlower
  </div>
  <div style="font-size: 1em; color: #666; margin-top: 1.5em;">
    David Sarrat Gonz&aacute;lez &nbsp;&middot;&nbsp; Juan R Gonz&aacute;lez
  </div>
  <div style="font-size: 0.85em; color: #444; margin-top: 0.3em;">
    ISGlobal &nbsp;&middot;&nbsp; Barcelona
  </div>
</div>
