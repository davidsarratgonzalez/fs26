## Server-Side Stack

<div style="margin-top: 0.2em;">
<svg viewBox="0 0 720 320" style="width: 100%; max-height: 410px;">

  <!-- ===== ALWAYS VISIBLE: Server box + DataSHIELD ecosystem + Patient Data ===== -->

  <!-- Outer server box -->
  <rect x="30" y="5" width="520" height="300" rx="14" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.10)" stroke-width="0.8"/>
  <text x="290" y="22" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="4" font-weight="500">Hospital Server</text>

  <!-- DataSHIELD ecosystem column (left) -->
  <rect x="50" y="32" width="130" height="220" rx="10" fill="rgba(255,255,255,0.06)" stroke="rgba(255,255,255,0.10)" stroke-width="0.8"/>
  <text x="115" y="50" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="3.5" font-weight="500">DataSHIELD</text>
  <text x="115" y="62" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="2.5">Ecosystem</text>
  <text x="115" y="82" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">dsBase</text>
  <text x="115" y="96" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">dsOmics</text>
  <text x="115" y="110" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">dsOMOP</text>
  <text x="115" y="124" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">dsSurvival</text>
  <text x="115" y="138" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">dsExposome</text>
  <text x="115" y="152" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">dsImaging</text>
  <text x="115" y="166" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">dsMicrobiome</text>
  <text x="115" y="182" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">...</text>
  <text x="115" y="205" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">Disclosure control</text>
  <text x="115" y="217" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">Non-disclosive only</text>
  <text x="115" y="229" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">Server-enforced</text>
  <text x="115" y="245" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">Sandboxed execution</text>

  <!-- Patient Data bar (bottom) -->
  <rect x="50" y="262" width="485" height="35" rx="8" fill="rgba(255,180,100,0.06)" stroke="rgba(255,180,100,0.12)" stroke-width="0.8"/>
  <text x="292" y="280" text-anchor="middle" fill="#ffb366" font-family="Roboto Mono" font-size="3.5">Patient Data</text>
  <text x="292" y="291" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">never leaves the server</text>

  <!-- ===== CLICK 1: dsFlower (interactor) ===== -->
  <g v-click>
    <rect x="200" y="32" width="335" height="42" rx="10" fill="rgba(255,208,0,0.06)" stroke="rgba(255,208,0,0.12)" stroke-width="0.8"/>
    <text x="367" y="50" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="3.8" font-weight="500">dsFlower (batteries-included)</text>
    <text x="367" y="65" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">SuperNode management · Remote orchestration</text>
  </g>

  <!-- ===== CLICK 2: SuperNode + analyst lines ===== -->
  <g v-click>
    <!-- SuperNode box (blue/prominent) -->
    <rect x="200" y="82" width="335" height="38" rx="8" fill="rgba(136,204,255,0.08)" stroke="rgba(136,204,255,0.20)" stroke-width="0.8"/>
    <text x="367" y="100" text-anchor="middle" fill="#88ccff" font-family="Roboto Mono" font-size="3.5" font-weight="500">Flower SuperNode</text>
    <text x="367" y="113" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">gRPC client, spawned on demand</text>

    <!-- Animated lines FROM SuperNode right edge to off-screen -->
    <path d="M535,95 L720,95" fill="none" stroke="#FFD000" stroke-width="2" stroke-dasharray="6 4">
      <animate attributeName="stroke-dashoffset" from="0" to="-10" dur="0.8s" repeatCount="indefinite"/>
    </path>
    <path d="M720,105 L535,105" fill="none" stroke="#66ddaa" stroke-width="2" stroke-dasharray="6 4">
      <animate attributeName="stroke-dashoffset" from="0" to="-10" dur="0.8s" repeatCount="indefinite"/>
    </path>

    <!-- Labels above/below lines -->
    <text x="628" y="91" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="2.2">weight updates →</text>
    <text x="628" y="116" text-anchor="middle" fill="#66ddaa" font-family="Roboto Mono" font-size="2.2">← global model</text>
    <text x="628" y="128" text-anchor="middle" fill="#88ccff" font-family="Roboto Mono" font-size="2.5">Analyst SuperLink</text>
  </g>

  <!-- ===== CLICK 3: Python environments ===== -->
  <g v-click>
    <rect x="200" y="128" width="335" height="55" rx="10" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.08)" stroke-width="0.8"/>
    <text x="367" y="143" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="2.8">Python environments (via uv)</text>

    <rect x="215" y="150" width="95" height="24" rx="4" fill="rgba(255,208,0,0.06)" stroke="rgba(255,208,0,0.10)" stroke-width="0.5"/>
    <text x="262" y="165" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="2.5">scikit-learn</text>

    <rect x="320" y="150" width="100" height="24" rx="4" fill="rgba(255,208,0,0.06)" stroke="rgba(255,208,0,0.10)" stroke-width="0.5"/>
    <text x="370" y="165" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="2.5">PyTorch + Opacus</text>

    <rect x="430" y="150" width="90" height="24" rx="4" fill="rgba(255,208,0,0.06)" stroke="rgba(255,208,0,0.10)" stroke-width="0.5"/>
    <text x="475" y="165" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="2.5">XGBoost</text>
  </g>

  <!-- ===== CLICK 4: Pre-approved Templates ===== -->
  <g v-click>
    <rect x="200" y="191" width="335" height="48" rx="10" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.08)" stroke-width="0.8"/>
    <text x="367" y="207" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="2.8">18 Pre-approved Templates (Flower Apps)</text>
    <text x="367" y="219" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">Common biomedical research operations</text>
    <text x="367" y="232" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">LogReg · MLP · ResNet-18 · U-Net · LSTM · Cox PH · XGBoost ...</text>
  </g>

  <!-- ===== CLICK 5: Security + protection line over the analyst connection ===== -->
  <g v-click>
    <!-- Trust profiles bar -->
    <rect x="200" y="246" width="335" height="14" rx="4" fill="rgba(102,221,170,0.06)" stroke="rgba(102,221,170,0.15)" stroke-width="0.5"/>
    <text x="367" y="256" text-anchor="middle" fill="#66ddaa" font-family="Roboto Mono" font-size="2.5">Trust profiles · SecAgg+ · DP-SGD · Disclosure control</text>

    <!-- Protection line over the analyst connection -->
    <rect x="533" y="87" width="190" height="24" rx="6" fill="none" stroke="rgba(102,221,170,0.25)" stroke-width="0.8" stroke-dasharray="3 2"/>
    <text x="628" y="84" text-anchor="middle" fill="#66ddaa" font-family="Roboto Mono" font-size="2">encrypted · disclosure-controlled</text>
  </g>

</svg>
</div>
