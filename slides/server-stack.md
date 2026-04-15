## Server-Side Stack
<span style="color: #b0b8c0; font-size: 0.6em;">Batteries-included</span>

<div style="margin-top: 0.2em;">
<svg viewBox="0 0 780 310" style="width: 100%; max-height: 370px;">

  <!-- ===== ALWAYS VISIBLE: Server box + DataSHIELD + Patient Data ===== -->

  <!-- Outer server box -->
  <rect x="30" y="5" width="580" height="280" rx="14" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.10)" stroke-width="0.8"/>
  <text x="320" y="22" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="4" font-weight="500">Hospital Server</text>

  <!-- DataSHIELD column (left, always visible) -->
  <rect x="50" y="32" width="140" height="200" rx="10" fill="rgba(255,255,255,0.06)" stroke="rgba(255,255,255,0.10)" stroke-width="0.8"/>
  <text x="120" y="50" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="3.8" font-weight="500">DataSHIELD</text>
  <text x="120" y="65" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">Aggregate methods</text>
  <text x="120" y="80" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">ds.glm()</text>
  <text x="120" y="90" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">ds.mean()</text>
  <text x="120" y="100" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">ds.var()</text>
  <text x="120" y="125" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">Assign methods</text>
  <text x="120" y="140" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">datashield.assign()</text>
  <text x="120" y="165" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">Disclosure control</text>
  <text x="120" y="180" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">Non-disclosive only</text>

  <!-- Patient Data bar (bottom, always visible) -->
  <rect x="50" y="242" width="545" height="35" rx="8" fill="rgba(255,180,100,0.06)" stroke="rgba(255,180,100,0.12)" stroke-width="0.8"/>
  <text x="322" y="260" text-anchor="middle" fill="#ffb366" font-family="Roboto Mono" font-size="3.5">Patient Data</text>
  <text x="322" y="272" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">never leaves the server</text>

  <!-- ===== CLICK 1: dsFlower R package ===== -->
  <g v-click>
    <rect x="210" y="32" width="385" height="55" rx="10" fill="rgba(255,208,0,0.06)" stroke="rgba(255,208,0,0.12)" stroke-width="0.8"/>
    <text x="402" y="52" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="3.8" font-weight="500">dsFlower (R package)</text>
    <text x="402" y="66" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">SuperNode management · Remote analyst orchestration</text>
    <text x="402" y="78" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">Data staging via manifest.json</text>

    <!-- Annotation -->
    <text x="640" y="48" fill="#88ccff" font-family="Roboto Mono" font-size="3">Server admin</text>
    <text x="640" y="58" fill="#88ccff" font-family="Roboto Mono" font-size="3">installs this</text>
  </g>

  <!-- ===== CLICK 2: Python environments ===== -->
  <g v-click>
    <rect x="210" y="95" width="385" height="65" rx="10" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.08)" stroke-width="0.8"/>
    <text x="402" y="110" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="3">Python environments (via uv)</text>

    <!-- scikit-learn -->
    <rect x="225" y="118" width="105" height="30" rx="5" fill="rgba(255,208,0,0.06)" stroke="rgba(255,208,0,0.10)" stroke-width="0.5"/>
    <text x="277" y="131" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="2.8">scikit-learn</text>
    <text x="277" y="141" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="1.8">weights exchange</text>

    <!-- PyTorch -->
    <rect x="340" y="118" width="105" height="30" rx="5" fill="rgba(255,208,0,0.06)" stroke="rgba(255,208,0,0.10)" stroke-width="0.5"/>
    <text x="392" y="131" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="2.8">PyTorch</text>
    <text x="392" y="141" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="1.8">weights + Opacus DP</text>

    <!-- XGBoost -->
    <rect x="455" y="118" width="125" height="30" rx="5" fill="rgba(255,208,0,0.06)" stroke="rgba(255,208,0,0.10)" stroke-width="0.5"/>
    <text x="517" y="131" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="2.8">XGBoost</text>
    <text x="517" y="141" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="1.8">histogram aggregation</text>

    <!-- Annotation -->
    <text x="640" y="110" fill="#88ccff" font-family="Roboto Mono" font-size="3">Zero system deps</text>
    <text x="640" y="120" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">uv bootstraps Python</text>
    <text x="640" y="130" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">isolated per framework</text>
  </g>

  <!-- ===== CLICK 3: Pre-approved templates ===== -->
  <g v-click>
    <rect x="210" y="168" width="385" height="50" rx="10" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.08)" stroke-width="0.8"/>
    <text x="402" y="184" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="3">18 Pre-approved Templates</text>
    <text x="402" y="196" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">Common operations in biomedical research</text>
    <text x="402" y="208" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="1.8">LogReg · MLP · ResNet-18 · U-Net · LSTM · Cox PH · XGBoost ...</text>

    <!-- Annotation -->
    <text x="640" y="180" fill="#88ccff" font-family="Roboto Mono" font-size="3">Only vetted code</text>
    <text x="640" y="190" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">no arbitrary execution</text>
    <text x="640" y="200" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">SHA-256 verified</text>
  </g>

  <!-- ===== CLICK 4: Security ===== -->
  <g v-click>
    <rect x="210" y="224" width="385" height="14" rx="4" fill="rgba(102,221,170,0.06)" stroke="rgba(102,221,170,0.15)" stroke-width="0.5"/>
    <text x="402" y="234" text-anchor="middle" fill="#66ddaa" font-family="Roboto Mono" font-size="2.5">Trust profiles · SecAgg+ · DP-SGD · Disclosure control</text>

    <!-- Annotation -->
    <text x="640" y="234" fill="#88ccff" font-family="Roboto Mono" font-size="3">Privacy by default</text>
  </g>

</svg>
</div>
