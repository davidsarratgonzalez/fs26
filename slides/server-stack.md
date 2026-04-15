## Server-Side Stack

<div style="margin-top: 0.2em;">
<svg viewBox="0 0 720 300" style="width: 100%; max-height: 400px;">

  <!-- ===== ALWAYS VISIBLE: Server box + DataSHIELD ecosystem + Patient Data ===== -->

  <!-- Outer server box -->
  <rect x="30" y="5" width="520" height="280" rx="14" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.10)" stroke-width="0.8"/>
  <text x="290" y="22" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="4" font-weight="500">Hospital Server</text>

  <!-- DataSHIELD ecosystem column (left) -->
  <rect x="50" y="32" width="130" height="200" rx="10" fill="rgba(255,255,255,0.06)" stroke="rgba(255,255,255,0.10)" stroke-width="0.8"/>
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
  <text x="115" y="200" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">Disclosure control</text>
  <text x="115" y="212" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">Non-disclosive only</text>
  <text x="115" y="224" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">Server-enforced</text>

  <!-- Patient Data bar (bottom) -->
  <rect x="50" y="242" width="485" height="35" rx="8" fill="rgba(255,180,100,0.06)" stroke="rgba(255,180,100,0.12)" stroke-width="0.8"/>
  <text x="292" y="260" text-anchor="middle" fill="#ffb366" font-family="Roboto Mono" font-size="3.5">Patient Data</text>
  <text x="292" y="272" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">never leaves the server</text>

  <!-- ===== CLICK 1: dsFlower (interactor) ===== -->
  <g v-click>
    <rect x="200" y="32" width="335" height="40" rx="10" fill="rgba(255,208,0,0.06)" stroke="rgba(255,208,0,0.12)" stroke-width="0.8"/>
    <text x="367" y="48" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="3.8" font-weight="500">dsFlower (batteries-included)</text>
    <text x="367" y="63" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">SuperNode management · Remote orchestration</text>
  </g>

  <!-- ===== CLICK 2: SuperNode + analyst lines ===== -->
  <g v-click>
    <!-- SuperNode box (blue/prominent) -->
    <rect x="200" y="80" width="335" height="35" rx="8" fill="rgba(136,204,255,0.08)" stroke="rgba(136,204,255,0.20)" stroke-width="0.8"/>
    <text x="367" y="97" text-anchor="middle" fill="#88ccff" font-family="Roboto Mono" font-size="3.5" font-weight="500">Flower SuperNode</text>
    <text x="367" y="108" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">gRPC client, spawned on demand</text>

    <!-- Animated lines from SuperNode edge to off-screen (analyst) -->
    <path d="M535,88 L720,88" fill="none" stroke="#FFD000" stroke-width="1.5" stroke-dasharray="6 4">
      <animate attributeName="stroke-dashoffset" from="0" to="-10" dur="0.8s" repeatCount="indefinite"/>
    </path>
    <path d="M720,98 L535,98" fill="none" stroke="#66ddaa" stroke-width="1.5" stroke-dasharray="6 4">
      <animate attributeName="stroke-dashoffset" from="0" to="-10" dur="0.8s" repeatCount="indefinite"/>
    </path>

    <!-- Labels along lines -->
    <text x="625" y="85" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="2.2">weight updates →</text>
    <text x="625" y="108" text-anchor="middle" fill="#66ddaa" font-family="Roboto Mono" font-size="2.2">← global model</text>
    <text x="625" y="120" text-anchor="middle" fill="#88ccff" font-family="Roboto Mono" font-size="2.5">Analyst SuperLink interaction</text>
  </g>

  <!-- ===== CLICK 3: Python environments ===== -->
  <g v-click>
    <rect x="200" y="122" width="335" height="50" rx="10" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.08)" stroke-width="0.8"/>
    <text x="367" y="136" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="2.8">Python environments (via uv)</text>

    <rect x="215" y="142" width="95" height="22" rx="4" fill="rgba(255,208,0,0.06)" stroke="rgba(255,208,0,0.10)" stroke-width="0.5"/>
    <text x="262" y="155" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="2.5">scikit-learn</text>

    <rect x="320" y="142" width="95" height="22" rx="4" fill="rgba(255,208,0,0.06)" stroke="rgba(255,208,0,0.10)" stroke-width="0.5"/>
    <text x="367" y="155" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="2.5">PyTorch + Opacus</text>

    <rect x="425" y="142" width="95" height="22" rx="4" fill="rgba(255,208,0,0.06)" stroke="rgba(255,208,0,0.10)" stroke-width="0.5"/>
    <text x="472" y="155" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="2.5">XGBoost</text>
  </g>

  <!-- ===== CLICK 4: Pre-approved Templates ===== -->
  <g v-click>
    <rect x="200" y="180" width="335" height="38" rx="10" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.08)" stroke-width="0.8"/>
    <text x="367" y="195" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="2.8">18 Pre-approved Templates (Flower Apps)</text>
    <text x="367" y="208" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">Common biomedical research: LogReg · MLP · ResNet-18 · Cox PH · XGBoost ...</text>
  </g>

  <!-- ===== CLICK 4: Security + protection line over the analyst connection ===== -->
  <g v-click>
    <!-- Trust profiles bar -->
    <rect x="200" y="224" width="335" height="14" rx="4" fill="rgba(102,221,170,0.06)" stroke="rgba(102,221,170,0.15)" stroke-width="0.5"/>
    <text x="367" y="234" text-anchor="middle" fill="#66ddaa" font-family="Roboto Mono" font-size="2.5">Trust profiles · SecAgg+ · DP-SGD · Disclosure control</text>

    <!-- Protection line over the analyst connection -->
    <rect x="533" y="80" width="190" height="24" rx="6" fill="none" stroke="rgba(102,221,170,0.25)" stroke-width="0.8" stroke-dasharray="3 2"/>
    <text x="628" y="76" text-anchor="middle" fill="#66ddaa" font-family="Roboto Mono" font-size="2">encrypted · disclosure-controlled</text>
  </g>

</svg>
</div>
