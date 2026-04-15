## Analyst-Side Package

<div style="position: relative; margin-top: 0.2em;">

<svg viewBox="0 -15 720 355" style="width: 100%; max-height: 430px;">

  <!-- ===== ALWAYS VISIBLE: Analyst machine ===== -->

  <!-- Analyst machine box -->
  <rect x="170" y="5" width="380" height="320" rx="14" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.10)" stroke-width="0.8"/>
  <text x="360" y="24" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="4" font-weight="500">Analyst Machine</text>

  <!-- ===== CLICK 1: dsFlowerClient ===== -->
  <g v-click>
    <rect x="195" y="36" width="330" height="44" rx="10" fill="rgba(255,208,0,0.06)" stroke="rgba(255,208,0,0.12)" stroke-width="0.8"/>
    <text x="360" y="54" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="3.8" font-weight="500">dsFlowerClient R Package</text>
    <text x="360" y="70" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">Run orchestration · Result management</text>
  </g>

  <!-- ===== CLICK 2: SuperLink ===== -->
  <g v-click>
    <rect x="195" y="90" width="330" height="40" rx="8" fill="rgba(136,204,255,0.08)" stroke="rgba(136,204,255,0.20)" stroke-width="0.8"/>
    <text x="360" y="108" text-anchor="middle" fill="#88ccff" font-family="Roboto Mono" font-size="3.5" font-weight="500">Flower SuperLink</text>
    <text x="360" y="123" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">gRPC coordinator, TLS certificates</text>

    <!-- Annotation: auto-discoverability -->
    <text x="560" y="100" fill="#88ccff" font-family="Roboto Mono" font-size="3">Auto-discovery</text>
    <text x="560" y="112" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">Detects reachable</text>
    <text x="560" y="122" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">address for nodes</text>
  </g>

  <!-- ===== CLICK 3: Template catalog ===== -->
  <g v-click>
    <rect x="195" y="140" width="330" height="42" rx="10" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.08)" stroke-width="0.8"/>
    <text x="360" y="157" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="2.8">Template Catalog Exploration</text>
    <text x="360" y="174" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">Query available models on each server</text>

    <text x="560" y="155" fill="#88ccff" font-family="Roboto Mono" font-size="3">flowerGetCapabilitiesDS()</text>
    <text x="560" y="167" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">Templates, trust profile,</text>
    <text x="560" y="177" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.2">server capabilities</text>
  </g>

  <!-- ===== CLICK 4: Recipe composition ===== -->
  <g v-click>
    <rect x="195" y="192" width="330" height="55" rx="10" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.08)" stroke-width="0.8"/>
    <text x="360" y="209" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="2.8">Composable Recipe</text>
    <text x="360" y="225" text-anchor="middle" fill="#FFD000" font-family="Roboto Mono" font-size="2.8">model + strategy + task</text>
    <text x="360" y="240" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2">20 models · 5 strategies · 4 task types</text>
  </g>

  <!-- ===== CLICK 5: Code integrity ===== -->
  <g v-click>
    <rect x="195" y="255" width="330" height="18" rx="5" fill="rgba(102,221,170,0.06)" stroke="rgba(102,221,170,0.15)" stroke-width="0.6"/>
    <text x="360" y="267" text-anchor="middle" fill="#66ddaa" font-family="Roboto Mono" font-size="2.2">Code integrity: SHA-256 verification against all servers</text>
  </g>

  <!-- Hospital indicators (right side, always visible) -->
  <rect x="30" y="90" width="120" height="30" rx="8" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.08)" stroke-width="0.6"/>
  <text x="90" y="107" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">N Hospital Servers</text>
  <text x="90" y="117" text-anchor="middle" fill="#b0b8c0" font-family="Roboto Mono" font-size="1.8">(dsFlower installed)</text>

</svg>

<!-- Animated connection lines (HTML, positioned over SVG) -->
<div v-click="2" class="marching-line marching-left" style="position:absolute; left:3.5%; top:33%; width:23%; height:3px;"></div>
<div v-click="2" class="marching-line marching-right" style="position:absolute; left:3.5%; top:37%; width:23%; height:3px;"></div>

</div>
