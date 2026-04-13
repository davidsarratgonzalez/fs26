---
theme: default
title: dsFlower
class: text-center
drawings:
  persist: false
transition: fade
css: unocss
---

<div class="flex flex-col items-center justify-center h-full">
  <div style="font-family: 'Roboto Mono', monospace; font-weight: 400; font-size: 4em; text-transform: uppercase;">
    ds<span style="color: #E09600;">Flower</span>
  </div>
  <div style="font-size: 1.2em; color: #666; margin-top: 0.4em;">
    Federated Learning for DataSHIELD
  </div>
  <div style="font-size: 0.9em; color: #999; margin-top: 0.2em;">
    Powered by <a href="https://flower.ai">flower.ai</a>
  </div>
  <div style="font-family: 'Roboto Mono', monospace; font-size: 0.75em; color: #999; margin-top: 2.5em;">
    David Sarrat Gonz&aacute;lez &nbsp;&middot;&nbsp; Juan R Gonz&aacute;lez<br/>
    <span style="color: #bbb;">ISGlobal &middot; Barcelona</span>
  </div>
</div>

---

## The problem

Hospitals want to train ML models together **without sharing patient data**.

<div class="grid grid-cols-2 gap-8 mt-6">
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

DataSHIELD handles orchestration. **Flower** handles weight transport via gRPC. Raw data stays on each hospital's server.

---

## How it works

<div class="grid grid-cols-3 gap-6 mt-8">
<div style="background: #fafafa; border: 1px solid #eee; border-radius: 6px; padding: 1.2em; text-align: center;">
  <div style="font-family: 'Roboto Mono'; font-size: 1.6em; color: #E09600;">1</div>
  <div style="font-family: 'Roboto Mono'; font-size: 0.8em; text-transform: uppercase;">Connect</div>
  <div style="font-size: 0.8em; color: #888; margin-top: 0.4em;">Researcher connects to N hospital nodes via DataSHIELD</div>
</div>
<div style="background: #fafafa; border: 1px solid #eee; border-radius: 6px; padding: 1.2em; text-align: center;">
  <div style="font-family: 'Roboto Mono'; font-size: 1.6em; color: #E09600;">2</div>
  <div style="font-family: 'Roboto Mono'; font-size: 0.8em; text-transform: uppercase;">Train</div>
  <div style="font-size: 0.8em; color: #888; margin-top: 0.4em;">Each node trains on local data, sends weight updates to SuperLink</div>
</div>
<div style="background: #fafafa; border: 1px solid #eee; border-radius: 6px; padding: 1.2em; text-align: center;">
  <div style="font-family: 'Roboto Mono'; font-size: 1.6em; color: #E09600;">3</div>
  <div style="font-family: 'Roboto Mono'; font-size: 0.8em; text-transform: uppercase;">Aggregate</div>
  <div style="font-size: 0.8em; color: #888; margin-top: 0.4em;">SuperLink averages updates, sends global model back. Repeat N rounds.</div>
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

---

## Models

<div class="grid grid-cols-2 gap-6 mt-2">
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

Each includes:
- `client_app.py` — training loop
- `server_app.py` — aggregation
- `task.py` — data loading
- `privacy_utils.py` — DP, clipping

The researcher picks a model. The server does the rest.

</div>
</div>

---

## Strategies

| Strategy | Description | When to use |
|---|---|---|
| **FedAvg** | Standard averaging | Default |
| **FedProx** | Proximal penalty term | Non-IID data across hospitals |
| **FedAdam** | Server-side Adam optimizer | Unstable convergence |
| **FedAdagrad** | Server-side Adagrad | Sparse features |
| **FedBN** | Excludes BatchNorm from aggregation | Different scanners per site |

```r
recipe <- ds.flower.recipe(
  model    = ds.flower.model.pytorch_resnet18(),
  strategy = ds.flower.strategy.fedbn(),
  ...
)
```

---

## Privacy model

Four layers of protection against an untrusted researcher:

<div class="grid grid-cols-2 gap-6 mt-4">
<div>

### Layer 1 — DataSHIELD
Raw data stays on the server. The researcher only calls approved methods.

### Layer 2 — SecAgg+
Individual weight updates are encrypted. The researcher only sees the **aggregate**.

</div>
<div>

### Layer 3 ��� DP-SGD
Each node adds calibrated noise before sending. Formal guarantees via Opacus.

### Layer 4 — Disclosure control
Bucketed counts, suppressed per-node metrics, minimum sample sizes.

</div>
</div>

---

## Privacy profiles

| Profile | SecAgg | DP | Min rows | Metrics | Use case |
|---|---|---|---|---|---|
| `sandbox_open` | | | 3 | per-node | Development |
| `trusted_internal` | | | 50 | per-node | Single institution |
| `consortium_internal` | yes | | 50 | aggregate | Multi-site |
| `clinical_default` | yes | | 100 | aggregate | Hospital deployment |
| `clinical_hardened` | yes | | 200 | aggregate | High security |
| `clinical_update_noise` | yes | noise | 200 | aggregate | Update-level DP |
| `high_sensitivity_dp` | yes | Opacus | 500 | aggregate | Patient-level DP |

Profiles are **server-enforced**. The researcher cannot bypass them.

---

## Demo: 3 hospitals, 3 algorithms

```r
conns <- datashield.login(builder$build(), assign = TRUE, symbol = "D")
flower <- ds.flower.connect(conns, symbol = "D")

# 1. Logistic Regression (scikit-learn)
r1 <- ds.flower.run(flower, ds.flower.recipe(
  model = ds.flower.model.sklearn_logreg(),
  target_column = "malignant", num_rounds = 5L))

# 2. MLP with FedProx (PyTorch)
r2 <- ds.flower.run(flower, ds.flower.recipe(
  model    = ds.flower.model.pytorch_mlp(hidden_layers = "32,16"),
  strategy = ds.flower.strategy.fedprox(proximal_mu = 0.1),
  target_column = "malignant", num_rounds = 5L))

# 3. XGBoost (secure histogram)
r3 <- ds.flower.run(flower, ds.flower.recipe(
  model = ds.flower.model.xgboost(max_depth = 4L),
  target_column = "malignant", num_rounds = 5L))
```

---

## Ecosystem

<div class="grid grid-cols-2 gap-8 mt-4">
<div>

### Server (each hospital)
| Package | Role |
|---|---|
| **dsFlower** | FL orchestration, privacy |
| **dsImaging** | Medical imaging (S3/MinIO) |
| **dsRadiomics** | Feature extraction |
| **dsJobs** | Durable job runtime |

</div>
<div>

### Client (researcher)
| Package | Role |
|---|---|
| **dsFlowerClient** | Recipes, training API |
| **dsImagingClient** | Dataset discovery |
| **dsRadiomicsClient** | Extraction workflows |
| **dsJobsClient** | Job monitoring |

</div>
</div>

---

<div class="flex flex-col items-center justify-center h-full">
  <div style="font-family: 'Roboto Mono', monospace; font-weight: 400; font-size: 3em; text-transform: uppercase;">
    ds<span style="color: #E09600;">Flower</span>
  </div>
  <div style="font-size: 1em; color: #666; margin-top: 0.5em;">
    github.com/isglobal-brge/dsFlower
  </div>
  <div style="font-size: 0.85em; color: #999; margin-top: 2em;">
    David Sarrat Gonz&aacute;lez &nbsp;&middot;&nbsp; Juan R Gonz&aacute;lez
  </div>
  <div style="font-size: 0.75em; color: #bbb; margin-top: 0.2em;">
    ISGlobal &middot; Barcelona
  </div>
</div>
