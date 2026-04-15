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
- `client_app.py` - training loop
- `server_app.py` - aggregation
- `task.py` - data loading
- `privacy_utils.py` - DP, clipping

The researcher picks a model. The server does the rest.

</div>
</div>
