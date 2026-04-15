## Server-Side Stack

<div style="margin-top: 0.3em;">
<svg viewBox="0 0 780 350" style="width: 100%; max-height: 400px;">

  <!-- Outer server box -->
  <rect x="60" y="10" width="520" height="330" rx="16" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.12)" stroke-width="1"/>
  <text x="320" y="30" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="4.5" font-weight="500">Hospital Server (Opal / Rock)</text>

  <!-- Layer 1: dsFlower R package -->
  <rect x="85" y="42" width="470" height="62" rx="10" fill="rgba(255,255,255,0.06)" stroke="rgba(255,255,255,0.10)" stroke-width="0.8"/>
  <text x="320" y="60" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="4" font-weight="500">dsFlower (R package)</text>
  <text x="320" y="73" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.8">DataSHIELD methods · Privacy policies · SuperNode management · Data staging</text>

  <!-- Arrow: spawns -->
  <line x1="320" y1="104" x2="320" y2="118" stroke="#e0d8d0" stroke-width="0.8" stroke-dasharray="2 2"/>
  <text x="340" y="113" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">spawns</text>

  <!-- Layer 2: Python venvs -->
  <rect x="85" y="120" width="470" height="72" rx="10" fill="rgba(255,255,255,0.06)" stroke="rgba(255,255,255,0.10)" stroke-width="0.8"/>
  <text x="320" y="137" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="3.5">Python environments (via uv)</text>

  <!-- Framework boxes -->
  <rect x="105" y="148" width="100" height="32" rx="6" fill="rgba(255,208,0,0.08)" stroke="rgba(255,208,0,0.15)" stroke-width="0.6"/>
  <text x="155" y="162" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="3">scikit-learn</text>
  <text x="155" y="172" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">+ Flower + NumPy</text>

  <rect x="225" y="148" width="100" height="32" rx="6" fill="rgba(255,208,0,0.08)" stroke="rgba(255,208,0,0.15)" stroke-width="0.6"/>
  <text x="275" y="162" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="3">PyTorch</text>
  <text x="275" y="172" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">+ Opacus + torchvision</text>

  <rect x="345" y="148" width="100" height="32" rx="6" fill="rgba(255,208,0,0.08)" stroke="rgba(255,208,0,0.15)" stroke-width="0.6"/>
  <text x="395" y="162" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="3">XGBoost</text>
  <text x="395" y="172" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">+ SecAgg histogram</text>

  <!-- Layer 3: Templates -->
  <rect x="85" y="204" width="470" height="62" rx="10" fill="rgba(255,255,255,0.06)" stroke="rgba(255,255,255,0.10)" stroke-width="0.8"/>
  <text x="320" y="222" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="3.5">18 Pre-approved Templates</text>
  <text x="320" y="235" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.8">client_app.py · server_app.py · task.py · privacy_utils.py</text>
  <text x="320" y="248" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">LogReg · MLP · ResNet-18 · U-Net · LSTM · Cox PH · ...</text>

  <!-- Layer 4: Patient data -->
  <rect x="85" y="278" width="470" height="48" rx="10" fill="rgba(255,180,100,0.06)" stroke="rgba(255,180,100,0.12)" stroke-width="0.8"/>
  <text x="320" y="300" text-anchor="middle" fill="#ffb366" font-family="Roboto Mono" font-size="3.5">Patient Data</text>
  <text x="320" y="313" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">never leaves the server</text>

  <!-- Right-side annotations -->
  <text x="610" y="70" fill="#88ccff" font-family="Roboto Mono" font-size="3.5">Zero system deps</text>
  <text x="610" y="80" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">uv bootstraps Python</text>

  <text x="610" y="155" fill="#88ccff" font-family="Roboto Mono" font-size="3.5">Isolated venvs</text>
  <text x="610" y="165" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">per ML framework</text>

  <text x="610" y="230" fill="#88ccff" font-family="Roboto Mono" font-size="3.5">Only vetted code</text>
  <text x="610" y="240" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">no arbitrary execution</text>

  <text x="610" y="305" fill="#88ccff" font-family="Roboto Mono" font-size="3.5">Privacy by default</text>
  <text x="610" y="315" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">trust profiles in manifests</text>

</svg>
</div>

`install.packages("dsFlower")` provisions the full stack. Researchers select from pre-approved templates.
