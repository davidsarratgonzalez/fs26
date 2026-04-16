## Strategies

| Strategy | Description | When to use |
|---|---|---|
| <span class="g-term" data-g="FedAvg">**FedAvg**</span> | Standard averaging | Default |
| <span class="g-term" data-g="FedProx">**FedProx**</span> | Proximal penalty term | Non-IID data across hospitals |
| <span class="g-term" data-g="FedAdam">**FedAdam**</span> | Server-side Adam optimizer | Unstable convergence |
| <span class="g-term" data-g="FedAdagrad">**FedAdagrad**</span> | Server-side Adagrad | Sparse features |
| <span class="g-term" data-g="FedBN">**FedBN**</span> | Excludes BatchNorm from aggregation | Different scanners per site |

<div style="margin-top: 1.5em;">

```r
recipe <- ds.flower.recipe(
  model    = ds.flower.model.pytorch_resnet18(),
  strategy = ds.flower.strategy.fedbn(),
  ...
)
```

</div>
