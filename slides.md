---
theme: default
title: dsFlower
class: text-center
drawings:
  persist: false
transition: slide-left
colorSchema: dark
css: unocss
---

<div class="flex flex-col items-center justify-center h-full">
  <div style="font-family: 'Roboto Mono', monospace; font-weight: 700; font-size: 4em; color: #000000;">
    ds<span class="flower-title">Flower</span>
  </div>
  <div style="font-size: 1.1em; color: #000000; margin-top: 0.3em; letter-spacing: 0.02em;">
    Privacy-Preserving Federated Learning for Biomedical Research
  </div>
  <div class="flex items-center justify-center gap-6" style="margin-top: 2em;">
    <div class="flex flex-col items-center gap-1">
      <img src="/david-sarrat.jpg" style="width: 64px; height: 64px; border-radius: 50%; object-fit: cover; border: 2px solid rgba(0,0,0,0.15);" />
      <span style="font-family: 'Roboto Mono', monospace; font-size: 0.8em; color: #333333;">David Sarrat Gonz&aacute;lez</span>
    </div>
    <div class="flex flex-col items-center gap-1">
      <img src="/juan-gonzalez.jpg" style="width: 64px; height: 64px; border-radius: 50%; object-fit: cover; border: 2px solid rgba(0,0,0,0.15);" />
      <span style="font-family: 'Roboto Mono', monospace; font-size: 0.8em; color: #333333;">Juan R Gonz&aacute;lez</span>
    </div>
  </div>
  <div class="flex flex-col items-center gap-3" style="margin-top: 1.2em; width: 420px;">
    <div class="flex items-center gap-4 " style="width: 100%;">
      <div class="logo-badge"><img src="/isglobal-logo.png" style="height: 34px;" /></div>
      <div class="logo-badge"><img src="/brge-logo.png" style="height: 38px;" /></div>
    </div>
    <div class="flex items-center gap-4 " style="width: 100%;">
      <div class="logo-badge"><img src="/datashield-logo.png" style="height: 32px;" /></div>
      <div class="logo-badge"><img src="/flower-logo.png" style="height: 30px;" /></div>
    </div>
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

<div style="margin-top: 0.5em;">
<svg viewBox="0 0 700 330" style="width: 100%; max-height: 380px;">

  <!-- Flow paths (defined once, drawn twice for bidirectional flow) -->
  <path id="pA" d="M350,72 C250,150 140,200 120,255" fill="none"/>
  <path id="pB" d="M350,72 L350,255" fill="none"/>
  <path id="pC" d="M350,72 C450,150 560,200 580,255" fill="none"/>

  <!-- Query flow — blue dashes flowing down -->
  <use href="#pA" class="flow-query"/>
  <use href="#pB" class="flow-query"/>
  <use href="#pC" class="flow-query"/>

  <!-- Result flow — lighter blue dashes flowing up -->
  <use href="#pA" class="flow-result"/>
  <use href="#pB" class="flow-result"/>
  <use href="#pC" class="flow-result"/>

  <!-- Flow labels -->
  <text x="210" y="148" fill="#1a3fff" font-family="Roboto Mono" font-size="9" opacity="0.8" transform="rotate(-28,210,148)">queries</text>
  <text x="470" y="148" fill="#1a3fff" font-family="Roboto Mono" font-size="9" opacity="0.8" transform="rotate(28,470,148)">queries</text>
  <text x="360" y="168" fill="#1a3fff" font-family="Roboto Mono" font-size="9" opacity="0.5">pooled results</text>

  <!-- Researcher node -->
  <g transform="translate(350,45)">
    <rect x="-75" y="-28" width="150" height="56" rx="12" class="node-card"/>
    <rect x="-10" y="-16" width="20" height="14" rx="2" fill="none" stroke="#333" stroke-width="1.5"/>
    <line x1="-14" y1="1" x2="14" y2="1" stroke="#333" stroke-width="2" stroke-linecap="round"/>
    <text y="20" text-anchor="middle" fill="#333" font-family="Roboto Mono" font-size="11" font-weight="500">Researcher</text>
  </g>

  <!-- Hospital A -->
  <g transform="translate(120,285)">
    <rect x="-75" y="-28" width="150" height="56" rx="12" class="node-card"/>
    <rect x="-10" y="-18" width="20" height="20" rx="2" fill="none" stroke="#333" stroke-width="1.5"/>
    <line x1="0" y1="-14" x2="0" y2="-4" stroke="#333" stroke-width="1.5"/>
    <line x1="-5" y1="-9" x2="5" y2="-9" stroke="#333" stroke-width="1.5"/>
    <text y="20" text-anchor="middle" fill="#333" font-family="Roboto Mono" font-size="11" font-weight="500">Hospital A</text>
  </g>

  <!-- Hospital B -->
  <g transform="translate(350,285)">
    <rect x="-75" y="-28" width="150" height="56" rx="12" class="node-card"/>
    <rect x="-10" y="-18" width="20" height="20" rx="2" fill="none" stroke="#333" stroke-width="1.5"/>
    <line x1="0" y1="-14" x2="0" y2="-4" stroke="#333" stroke-width="1.5"/>
    <line x1="-5" y1="-9" x2="5" y2="-9" stroke="#333" stroke-width="1.5"/>
    <text y="20" text-anchor="middle" fill="#333" font-family="Roboto Mono" font-size="11" font-weight="500">Hospital B</text>
  </g>

  <!-- Hospital C -->
  <g transform="translate(580,285)">
    <rect x="-75" y="-28" width="150" height="56" rx="12" class="node-card"/>
    <rect x="-10" y="-18" width="20" height="20" rx="2" fill="none" stroke="#333" stroke-width="1.5"/>
    <line x1="0" y1="-14" x2="0" y2="-4" stroke="#333" stroke-width="1.5"/>
    <line x1="-5" y1="-9" x2="5" y2="-9" stroke="#333" stroke-width="1.5"/>
    <text y="20" text-anchor="middle" fill="#333" font-family="Roboto Mono" font-size="11" font-weight="500">Hospital C</text>
  </g>

</svg>
</div>

Data **never leaves** the hospital. Only aggregated results travel back via DataSHIELD.

---

## How it works

<div class="grid grid-cols-3 gap-6 mt-8">
<div class="step-card" style="text-align: center;">
  <div style="font-family: 'Roboto Mono'; font-size: 1.6em; color: #FFD000;">1</div>
  <div style="font-family: 'Roboto Mono'; font-size: 0.8em; text-transform: uppercase; color: #f0e8e0; letter-spacing: 0.05em;">Connect</div>
  <div style="font-size: 0.8em; color: #a89888; margin-top: 0.4em;">Researcher connects to N hospital nodes via DataSHIELD</div>
</div>
<div class="step-card" style="text-align: center;">
  <div style="font-family: 'Roboto Mono'; font-size: 1.6em; color: #FFD000;">2</div>
  <div style="font-family: 'Roboto Mono'; font-size: 0.8em; text-transform: uppercase; color: #f0e8e0; letter-spacing: 0.05em;">Train</div>
  <div style="font-size: 0.8em; color: #a89888; margin-top: 0.4em;">Each node trains on local data, sends weight updates to SuperLink</div>
</div>
<div class="step-card" style="text-align: center;">
  <div style="font-family: 'Roboto Mono'; font-size: 1.6em; color: #FFD000;">3</div>
  <div style="font-family: 'Roboto Mono'; font-size: 0.8em; text-transform: uppercase; color: #f0e8e0; letter-spacing: 0.05em;">Aggregate</div>
  <div style="font-size: 0.8em; color: #a89888; margin-top: 0.4em;">SuperLink averages updates, sends global model back. Repeat N rounds.</div>
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

### Layer 3 — DP-SGD
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
  <div style="font-family: 'Montserrat', sans-serif; font-weight: 700; font-size: 2.5em; color: #000000;">
    Thank you for your attention!
  </div>
  <div style="font-family: 'Roboto Mono', monospace; font-size: 0.9em; color: #000000; margin-top: 0.3em;">
    <a href="https://github.com/isglobal-brge/dsFlower" style="color: #1a3fff !important; text-decoration: none !important;">github.com/isglobal-brge/dsFlower</a>
  </div>
  <div class="flex items-center justify-center gap-6" style="margin-top: 2em;">
    <div class="flex flex-col items-center gap-1">
      <img src="/david-sarrat.jpg" style="width: 64px; height: 64px; border-radius: 50%; object-fit: cover; border: 2px solid rgba(0,0,0,0.15);" />
      <span style="font-family: 'Roboto Mono', monospace; font-size: 0.8em; color: #333333;">David Sarrat Gonz&aacute;lez</span>
      <a href="mailto:david.sarrat@isglobal.org" style="font-family: 'Roboto Mono', monospace; font-size: 0.7em; color: #1a3fff !important; text-decoration: none;">david.sarrat@isglobal.org</a>
    </div>
    <div class="flex flex-col items-center gap-1">
      <img src="/juan-gonzalez.jpg" style="width: 64px; height: 64px; border-radius: 50%; object-fit: cover; border: 2px solid rgba(0,0,0,0.15);" />
      <span style="font-family: 'Roboto Mono', monospace; font-size: 0.8em; color: #333333;">Juan R Gonz&aacute;lez</span>
      <a href="mailto:juanr.gonzalez@isglobal.org" style="font-family: 'Roboto Mono', monospace; font-size: 0.7em; color: #1a3fff !important; text-decoration: none;">juanr.gonzalez@isglobal.org</a>
    </div>
  </div>
  <div class="flex flex-col items-center gap-3" style="margin-top: 1.4em; width: 420px;">
    <div class="flex items-center gap-4 " style="width: 100%;">
      <div class="logo-badge"><img src="/isglobal-logo.png" style="height: 34px;" /></div>
      <div class="logo-badge"><img src="/brge-logo.png" style="height: 38px;" /></div>
    </div>
    <div class="flex items-center gap-4 " style="width: 100%;">
      <div class="logo-badge"><img src="/datashield-logo.png" style="height: 32px;" /></div>
      <div class="logo-badge"><img src="/flower-logo.png" style="height: 30px;" /></div>
    </div>
  </div>
</div>
