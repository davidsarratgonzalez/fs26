## Server-Side Stack

<div style="margin-top: 0.2em;">
<svg viewBox="0 0 820 310" style="width: 100%; max-height: 370px;">

  <!-- ===== ALWAYS VISIBLE: Server box + DataSHIELD ecosystem + Patient Data ===== -->

  <!-- Outer server box -->
  <rect x="30" y="5" width="560" height="280" rx="14" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.10)" stroke-width="0.8"/>
  <text x="310" y="22" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="4" font-weight="500">Hospital Server</text>

  <!-- DataSHIELD ecosystem column (left, always visible) -->
  <rect x="50" y="32" width="140" height="200" rx="10" fill="rgba(255,255,255,0.06)" stroke="rgba(255,255,255,0.10)" stroke-width="0.8"/>
  <text x="120" y="50" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="3.5" font-weight="500">DataSHIELD</text>
  <text x="120" y="62" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">Ecosystem</text>

  <text x="120" y="82" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">dsBase</text>
  <text x="120" y="96" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">dsOmics</text>
  <text x="120" y="110" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">dsOMOP</text>
  <text x="120" y="124" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">dsSurvival</text>
  <text x="120" y="138" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">dsExposome</text>
  <text x="120" y="152" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">dsImaging</text>
  <text x="120" y="166" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">dsMicrobiome</text>
  <text x="120" y="182" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">...</text>

  <text x="120" y="200" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">Disclosure control</text>
  <text x="120" y="212" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">Non-disclosive only</text>
  <text x="120" y="224" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">Server-enforced</text>

  <!-- Patient Data bar (bottom, always visible) -->
  <rect x="50" y="242" width="525" height="35" rx="8" fill="rgba(255,180,100,0.06)" stroke="rgba(255,180,100,0.12)" stroke-width="0.8"/>
  <text x="312" y="260" text-anchor="middle" fill="#ffb366" font-family="Roboto Mono" font-size="3.5">Patient Data</text>
  <text x="312" y="272" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">never leaves the server</text>

  <!-- ===== CLICK 1: dsFlower R package + analyst lines ===== -->
  <g v-click>
    <rect x="210" y="32" width="365" height="55" rx="10" fill="rgba(255,208,0,0.06)" stroke="rgba(255,208,0,0.12)" stroke-width="0.8"/>
    <text x="392" y="52" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="3.8" font-weight="500">dsFlower (R package)</text>
    <text x="392" y="66" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">SuperNode management · Remote orchestration</text>
    <text x="392" y="78" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">Data staging via manifest.json</text>

    <!-- Animated lines to analyst (right side) -->
    <path d="M575,50 C620,50 650,42 720,42" fill="none" stroke="#FFD000" stroke-width="1.5" stroke-dasharray="6 4">
      <animate attributeName="stroke-dashoffset" from="0" to="-10" dur="0.8s" repeatCount="indefinite"/>
    </path>
    <path d="M720,62 C650,62 620,55 575,55" fill="none" stroke="#66ddaa" stroke-width="1.5" stroke-dasharray="6 4">
      <animate attributeName="stroke-dashoffset" from="0" to="-10" dur="0.8s" repeatCount="indefinite"/>
    </path>

    <!-- Analyst label -->
    <text x="740" y="42" fill="#88ccff" font-family="Roboto Mono" font-size="3">Analyst-side</text>
    <text x="740" y="52" fill="#88ccff" font-family="Roboto Mono" font-size="3">interaction</text>
    <text x="740" y="66" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">via DataSHIELD</text>
  </g>

  <!-- ===== CLICK 2: Python environments ===== -->
  <g v-click>
    <rect x="210" y="95" width="365" height="62" rx="10" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.08)" stroke-width="0.8"/>
    <text x="392" y="110" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="3">Python environments (via uv)</text>

    <!-- scikit-learn -->
    <rect x="225" y="117" width="100" height="28" rx="5" fill="rgba(255,208,0,0.06)" stroke="rgba(255,208,0,0.10)" stroke-width="0.5"/>
    <text x="275" y="129" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="2.8">scikit-learn</text>
    <text x="275" y="139" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="1.8">weights exchange</text>

    <!-- PyTorch -->
    <rect x="335" y="117" width="100" height="28" rx="5" fill="rgba(255,208,0,0.06)" stroke="rgba(255,208,0,0.10)" stroke-width="0.5"/>
    <text x="385" y="129" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="2.8">PyTorch</text>
    <text x="385" y="139" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="1.8">weights + Opacus DP</text>

    <!-- XGBoost -->
    <rect x="445" y="117" width="115" height="28" rx="5" fill="rgba(255,208,0,0.06)" stroke="rgba(255,208,0,0.10)" stroke-width="0.5"/>
    <text x="502" y="129" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="2.8">XGBoost</text>
    <text x="502" y="139" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="1.8">histogram aggregation</text>

    <!-- Annotation -->
    <text x="640" y="115" fill="#88ccff" font-family="Roboto Mono" font-size="3">Zero system deps</text>
    <text x="640" y="126" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">uv bootstraps Python</text>
    <text x="640" y="136" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">isolated per framework</text>
  </g>

  <!-- ===== CLICK 3: Pre-approved templates ===== -->
  <g v-click>
    <rect x="210" y="165" width="365" height="48" rx="10" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.08)" stroke-width="0.8"/>
    <text x="392" y="180" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="3">18 Pre-approved Templates</text>
    <text x="392" y="192" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">Common operations in biomedical research</text>
    <text x="392" y="204" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="1.8">LogReg · MLP · ResNet-18 · U-Net · LSTM · Cox PH · XGBoost ...</text>

    <!-- Annotation -->
    <text x="640" y="178" fill="#88ccff" font-family="Roboto Mono" font-size="3">Only vetted code</text>
    <text x="640" y="189" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">no arbitrary execution</text>
    <text x="640" y="199" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">SHA-256 verified</text>
  </g>

  <!-- ===== CLICK 4: Security ===== -->
  <g v-click>
    <rect x="210" y="220" width="365" height="14" rx="4" fill="rgba(102,221,170,0.06)" stroke="rgba(102,221,170,0.15)" stroke-width="0.5"/>
    <text x="392" y="230" text-anchor="middle" fill="#66ddaa" font-family="Roboto Mono" font-size="2.5">Trust profiles · SecAgg+ · DP-SGD · Disclosure control</text>

    <text x="640" y="230" fill="#88ccff" font-family="Roboto Mono" font-size="3">Privacy by default</text>
  </g>

</svg>
</div>
