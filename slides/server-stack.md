## Server-Side Stack

<div style="margin-top: 0.2em;">
<svg viewBox="0 0 720 350" style="width: 100%; max-height: 430px;">

  <!-- ===== ALWAYS VISIBLE: Server box + DataSHIELD ecosystem + Patient Data ===== -->

  <!-- Outer server box -->
  <rect x="30" y="5" width="520" height="330" rx="14" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.10)" stroke-width="0.8"/>
  <text x="290" y="24" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="4" font-weight="500">Hospital Server (DataSHIELD)</text>

  <!-- DataSHIELD ecosystem column (left) -->
  <rect x="50" y="36" width="130" height="240" rx="10" fill="rgba(255,255,255,0.06)" stroke="rgba(255,255,255,0.10)" stroke-width="0.8"/>
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
  <text x="115" y="215" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">Disclosure control</text>
  <text x="115" y="228" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">Non-disclosive only</text>
  <text x="115" y="241" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">Server-enforced</text>
  <text x="115" y="254" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">Sandboxed execution</text>
  <text x="115" y="270" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">...</text>

  <!-- Patient Data bar (bottom) -->
  <rect x="50" y="286" width="485" height="40" rx="8" fill="rgba(255,180,100,0.06)" stroke="rgba(255,180,100,0.12)" stroke-width="0.8"/>
  <text x="292" y="306" text-anchor="middle" fill="#ffb366" font-family="Roboto Mono" font-size="3.5">Patient Data</text>
  <text x="292" y="318" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">never leaves the server</text>

  <!-- ===== CLICK 1: dsFlower ===== -->
  <g v-click>
    <rect x="200" y="36" width="335" height="46" rx="10" fill="rgba(255,208,0,0.06)" stroke="rgba(255,208,0,0.12)" stroke-width="0.8"/>
    <text x="367" y="55" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="3.8" font-weight="500">dsFlower (batteries-included)</text>
    <text x="367" y="72" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">SuperNode management · Remote orchestration</text>
  </g>

  <!-- ===== CLICK 2: SuperNode + analyst lines (CSS animated) ===== -->
  <g v-click>
    <!-- SuperNode box -->
    <rect x="200" y="90" width="335" height="40" rx="8" fill="rgba(136,204,255,0.08)" stroke="rgba(136,204,255,0.20)" stroke-width="0.8"/>
    <text x="367" y="109" text-anchor="middle" fill="#88ccff" font-family="Roboto Mono" font-size="3.5" font-weight="500">Flower SuperNode</text>
    <text x="367" y="123" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">gRPC client, spawned on demand</text>

    <!-- Analyst box (right, outside server) -->
    <rect x="600" y="90" width="110" height="40" rx="8" fill="rgba(136,204,255,0.06)" stroke="rgba(136,204,255,0.15)" stroke-width="0.8"/>
    <text x="655" y="109" text-anchor="middle" fill="#88ccff" font-family="Roboto Mono" font-size="3">Analyst</text>
    <text x="655" y="122" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">SuperLink</text>

    <!-- Animated line: weights out (CSS class) -->
    <line x1="535" y1="103" x2="600" y2="103" class="line-out"/>
    <text x="567" y="99" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="2">weights →</text>

    <!-- Animated line: model back (CSS class) -->
    <line x1="600" y1="117" x2="535" y2="117" class="line-in"/>
    <text x="567" y="127" text-anchor="middle" fill="#66ddaa" font-family="Roboto Mono" font-size="2">← model</text>
  </g>

  <!-- ===== CLICK 3: Python environments ===== -->
  <g v-click>
    <rect x="200" y="138" width="335" height="60" rx="10" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.08)" stroke-width="0.8"/>
    <text x="367" y="154" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="2.8">Python environments (via uv)</text>

    <rect x="215" y="162" width="95" height="26" rx="4" fill="rgba(255,208,0,0.06)" stroke="rgba(255,208,0,0.10)" stroke-width="0.5"/>
    <text x="262" y="178" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="2.5">scikit-learn</text>

    <rect x="320" y="162" width="100" height="26" rx="4" fill="rgba(255,208,0,0.06)" stroke="rgba(255,208,0,0.10)" stroke-width="0.5"/>
    <text x="370" y="178" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="2.5">PyTorch + Opacus</text>

    <rect x="430" y="162" width="90" height="26" rx="4" fill="rgba(255,208,0,0.06)" stroke="rgba(255,208,0,0.10)" stroke-width="0.5"/>
    <text x="475" y="178" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="2.5">XGBoost</text>
  </g>

  <!-- ===== CLICK 4: Pre-approved Templates ===== -->
  <g v-click>
    <rect x="200" y="206" width="335" height="52" rx="10" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.08)" stroke-width="0.8"/>
    <text x="367" y="224" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="2.8">18 Pre-approved Templates (Flower Apps)</text>
    <text x="367" y="238" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">Common biomedical research operations</text>
    <text x="367" y="250" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">LogReg · MLP · ResNet-18 · U-Net · LSTM · Cox PH · XGBoost ...</text>
  </g>

  <!-- ===== CLICK 5: Security + protection line ===== -->
  <g v-click>
    <!-- Trust profiles bar -->
    <rect x="200" y="266" width="335" height="16" rx="4" fill="rgba(102,221,170,0.06)" stroke="rgba(102,221,170,0.15)" stroke-width="0.5"/>
    <text x="367" y="278" text-anchor="middle" fill="#66ddaa" font-family="Roboto Mono" font-size="2.5">Trust profiles · SecAgg+ · DP-SGD · Disclosure control</text>

    <!-- Protection border around analyst connection -->
    <rect x="530" y="94" width="185" height="40" rx="6" fill="none" stroke="rgba(102,221,170,0.30)" stroke-width="1" stroke-dasharray="3 2"/>
    <text x="622" y="90" text-anchor="middle" fill="#66ddaa" font-family="Roboto Mono" font-size="2">encrypted · disclosure-controlled</text>
  </g>

</svg>
</div>
