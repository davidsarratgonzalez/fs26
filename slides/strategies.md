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
