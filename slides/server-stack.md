## Server-Side Package

<div style="position: relative; margin-top: 0.2em;">

<!-- Main SVG diagram -->
<svg viewBox="0 -15 720 355" style="width: 100%; max-height: 430px;">

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
  <text x="115" y="230" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">Sandboxed execution</text>
  <text x="115" y="250" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">...</text>

  <!-- Patient Data bar (bottom) -->
  <rect x="50" y="278" width="485" height="38" rx="8" fill="rgba(255,180,100,0.06)" stroke="rgba(255,180,100,0.12)" stroke-width="0.8"/>
  <text x="292" y="297" text-anchor="middle" fill="#ffb366" font-family="Roboto Mono" font-size="3.5">Patient Data</text>
  <text x="292" y="310" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">never leaves the server</text>

  <!-- ===== CLICK 1: dsFlower ===== -->
  <g v-click>
    <rect x="200" y="36" width="335" height="44" rx="10" fill="rgba(255,208,0,0.06)" stroke="rgba(255,208,0,0.12)" stroke-width="0.8"/>
    <text x="367" y="54" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="3.8" font-weight="500">dsFlower R Package</text>
    <text x="367" y="70" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">SuperNode management · Remote orchestration</text>
  </g>

  <!-- ===== CLICK 2: SuperNode (SVG only, lines are HTML below) ===== -->
  <g v-click>
    <rect x="200" y="90" width="335" height="40" rx="8" fill="rgba(136,204,255,0.08)" stroke="rgba(136,204,255,0.20)" stroke-width="0.8"/>
    <text x="367" y="108" text-anchor="middle" fill="#88ccff" font-family="Roboto Mono" font-size="3.5" font-weight="500">Flower SuperNode</text>
    <text x="367" y="123" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">gRPC client, spawned on demand</text>
  </g>

  <!-- ===== CLICK 3: Python environments ===== -->
  <g v-click>
    <rect x="200" y="140" width="335" height="42" rx="10" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.08)" stroke-width="0.8"/>
    <text x="367" y="157" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="2.8">Python environments (via uv)</text>
    <text x="367" y="174" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="2.8">scikit-learn · PyTorch + Opacus · XGBoost</text>
  </g>

  <!-- ===== CLICK 4: Templates ===== -->
  <g v-click>
    <rect x="200" y="190" width="335" height="52" rx="10" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.08)" stroke-width="0.8"/>
    <text x="367" y="208" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="2.8">18 Pre-approved Templates (Flower Apps)</text>
    <text x="367" y="222" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">Common biomedical research operations</text>
    <text x="367" y="235" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">LogReg · MLP · ResNet-18 · U-Net · LSTM · Cox PH · XGBoost ...</text>
  </g>

  <!-- ===== CLICK 5: Security (SVG part) ===== -->
  <g v-click>
    <rect x="200" y="248" width="335" height="18" rx="5" fill="rgba(102,221,170,0.06)" stroke="rgba(102,221,170,0.15)" stroke-width="0.6"/>
    <text x="367" y="260" text-anchor="middle" fill="#66ddaa" font-family="Roboto Mono" font-size="2.2">Trust profiles · SecAgg+ · DP-SGD · Disclosure control</text>
  </g>

</svg>

<!-- ===== CONNECTION LINES + ANALYST BOX (HTML, outside SVG) ===== -->
<!-- These are positioned absolutely over the SVG to guarantee rendering with v-click -->

<div v-click="2" style="position:absolute; top:28%; right:3%; display:flex; align-items:center; gap:6px;">
  <!-- Lines -->
  <div style="display:flex; flex-direction:column; gap:10px; width:50px;">
    <div style="position:relative;">
      <div style="height:3px; background:#FFD000; border-radius:2px;"></div>
      <span style="position:absolute; top:-14px; left:0; right:0; text-align:center; font-family:'Roboto Mono',monospace; font-size:0.45em; color:#FFD000;">weights →</span>
    </div>
    <div style="position:relative;">
      <div style="height:3px; background:#66ddaa; border-radius:2px;"></div>
      <span style="position:absolute; bottom:-14px; left:0; right:0; text-align:center; font-family:'Roboto Mono',monospace; font-size:0.45em; color:#66ddaa;">← model</span>
    </div>
  </div>
  <!-- Analyst box -->
  <div style="border:1px solid rgba(136,204,255,0.2); background:rgba(136,204,255,0.06); border-radius:8px; padding:8px 14px; text-align:center;">
    <div style="font-family:'Roboto Mono',monospace; font-size:0.65em; color:#88ccff; font-weight:500;">Analyst</div>
    <div style="font-family:'Roboto Mono',monospace; font-size:0.5em; color:#b0b8c0;">SuperLink</div>
  </div>
</div>

<!-- Protection border (appears on click 5) -->
<div v-click="5" style="position:absolute; top:26%; right:2%; width:180px; height:60px; border:1px dashed rgba(102,221,170,0.3); border-radius:8px;">
  <span style="position:absolute; top:-12px; left:50%; transform:translateX(-50%); font-family:'Roboto Mono',monospace; font-size:0.42em; color:#66ddaa;">encrypted · disclosure-controlled</span>
</div>

</div>
