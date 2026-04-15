## Server-Side Stack

<div style="margin-top: 0.2em;">
<svg viewBox="0 0 720 340" style="width: 100%; max-height: 430px;">

  <!-- ===== ALWAYS VISIBLE ===== -->

  <!-- Outer server box -->
  <rect x="30" y="5" width="520" height="320" rx="14" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.10)" stroke-width="0.8"/>
  <text x="290" y="24" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="4" font-weight="500">Hospital Server (DataSHIELD)</text>

  <!-- DataSHIELD ecosystem column (left) -->
  <rect x="50" y="36" width="130" height="230" rx="10" fill="rgba(255,255,255,0.06)" stroke="rgba(255,255,255,0.10)" stroke-width="0.8"/>
  <text x="115" y="56" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="3.5" font-weight="500">DataSHIELD</text>
  <text x="115" y="68" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="2.5">Ecosystem</text>
  <text x="115" y="90" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">dsBase</text>
  <text x="115" y="104" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">dsOmics</text>
  <text x="115" y="118" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">dsOMOP</text>
  <text x="115" y="132" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">dsSurvival</text>
  <text x="115" y="146" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">dsExposome</text>
  <text x="115" y="160" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">dsImaging</text>
  <text x="115" y="174" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">dsMicrobiome</text>
  <text x="115" y="190" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">...</text>
  <text x="115" y="215" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">Non-disclosive results</text>
  <text x="115" y="230" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">Server-enforced</text>
  <text x="115" y="245" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">Sandboxed execution</text>
  <text x="115" y="260" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">...</text>

  <!-- Patient Data bar (bottom) -->
  <rect x="50" y="278" width="485" height="38" rx="8" fill="rgba(255,180,100,0.06)" stroke="rgba(255,180,100,0.12)" stroke-width="0.8"/>
  <text x="292" y="297" text-anchor="middle" fill="#ffb366" font-family="Roboto Mono" font-size="3.5">Patient Data</text>
  <text x="292" y="310" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">never leaves the server</text>

  <!-- ===== CLICK 1: dsFlower ===== -->
  <g v-click>
    <rect x="200" y="36" width="335" height="44" rx="10" fill="rgba(255,208,0,0.06)" stroke="rgba(255,208,0,0.12)" stroke-width="0.8"/>
    <text x="367" y="54" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="3.8" font-weight="500">dsFlower (batteries-included)</text>
    <text x="367" y="70" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">SuperNode management · Remote orchestration</text>
  </g>

  <!-- ===== CLICK 2: SuperNode + connection bars ===== -->
  <g v-click>
    <rect x="200" y="88" width="335" height="38" rx="8" fill="rgba(136,204,255,0.08)" stroke="rgba(136,204,255,0.20)" stroke-width="0.8"/>
    <text x="367" y="106" text-anchor="middle" fill="#88ccff" font-family="Roboto Mono" font-size="3.5" font-weight="500">Flower SuperNode</text>
    <text x="367" y="120" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">gRPC client, spawned on demand</text>

    <!-- Analyst box -->
    <rect x="600" y="88" width="110" height="38" rx="8" fill="rgba(136,204,255,0.06)" stroke="rgba(136,204,255,0.15)" stroke-width="0.8"/>
    <text x="655" y="106" text-anchor="middle" fill="#88ccff" font-family="Roboto Mono" font-size="3">Analyst</text>
    <text x="655" y="119" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">SuperLink</text>

    <!-- Solid connection bars (rect guaranteed to render) -->
    <rect x="535" y="101" width="65" height="2.5" rx="1" fill="#FFD000"/>
    <text x="567" y="99" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="2">weights →</text>
    <rect x="535" y="115" width="65" height="2.5" rx="1" fill="#66ddaa"/>
    <text x="567" y="127" text-anchor="middle" fill="#66ddaa" font-family="Roboto Mono" font-size="2">← model</text>
  </g>

  <!-- ===== CLICK 3: Python environments ===== -->
  <g v-click>
    <rect x="200" y="134" width="335" height="40" rx="10" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.08)" stroke-width="0.8"/>
    <text x="367" y="150" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="2.8">Python environments (via uv)</text>
    <text x="367" y="166" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="2.8">scikit-learn · PyTorch + Opacus · XGBoost</text>
  </g>

  <!-- ===== CLICK 4: Templates ===== -->
  <g v-click>
    <rect x="200" y="180" width="335" height="50" rx="10" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.08)" stroke-width="0.8"/>
    <text x="367" y="197" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="2.8">18 Pre-approved Templates (Flower Apps)</text>
    <text x="367" y="211" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">Common biomedical research operations</text>
    <text x="367" y="224" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">LogReg · MLP · ResNet-18 · U-Net · LSTM · Cox PH · XGBoost ...</text>
  </g>

  <!-- ===== CLICK 5: Security ===== -->
  <g v-click>
    <rect x="200" y="236" width="335" height="26" rx="6" fill="rgba(102,221,170,0.06)" stroke="rgba(102,221,170,0.15)" stroke-width="0.6"/>
    <text x="367" y="253" text-anchor="middle" fill="#66ddaa" font-family="Roboto Mono" font-size="2.2">Trust profiles · SecAgg+ · DP-SGD · Disclosure control</text>

    <!-- Protection border around connection -->
    <rect x="530" y="94" width="185" height="38" rx="6" fill="none" stroke="rgba(102,221,170,0.30)" stroke-width="1" stroke-dasharray="3 2"/>
    <text x="622" y="90" text-anchor="middle" fill="#66ddaa" font-family="Roboto Mono" font-size="2">encrypted · disclosure-controlled</text>
  </g>

</svg>
</div>
