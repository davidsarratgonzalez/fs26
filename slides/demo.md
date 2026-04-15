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
