## dsFlower Workflow

<div style="margin-top: 0.5em;">
<svg viewBox="0 0 810 340" style="width: 100%; max-height: 390px;">

  <!-- SuperNode nodes (top row) -->
  <g transform="translate(120,65)">
    <rect x="-80" y="-40" width="160" height="80" rx="14" fill="rgba(136,204,255,0.08)" stroke="rgba(136,204,255,0.20)" stroke-width="1"/>
    <text y="-4" text-anchor="middle" fill="#88ccff" font-family="Roboto Mono" font-size="5" font-weight="500">SuperNode</text>
    <text y="14" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="4" font-weight="500">Hospital A</text>
    <text y="28" text-anchor="middle" fill="#ffb366" font-family="Roboto Mono" font-size="2.8">own data</text>
  </g>

  <g transform="translate(350,65)">
    <rect x="-80" y="-40" width="160" height="80" rx="14" fill="rgba(136,204,255,0.08)" stroke="rgba(136,204,255,0.20)" stroke-width="1"/>
    <text y="-4" text-anchor="middle" fill="#88ccff" font-family="Roboto Mono" font-size="5" font-weight="500">SuperNode</text>
    <text y="14" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="4" font-weight="500">Hospital B</text>
    <text y="28" text-anchor="middle" fill="#ffb366" font-family="Roboto Mono" font-size="2.8">own data</text>
  </g>

  <g transform="translate(580,65)">
    <rect x="-80" y="-40" width="160" height="80" rx="14" fill="rgba(136,204,255,0.08)" stroke="rgba(136,204,255,0.20)" stroke-width="1"/>
    <text y="-4" text-anchor="middle" fill="#88ccff" font-family="Roboto Mono" font-size="5" font-weight="500">SuperNode</text>
    <text y="14" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="4" font-weight="500">Hospital C</text>
    <text y="28" text-anchor="middle" fill="#ffb366" font-family="Roboto Mono" font-size="2.8">own data</text>
  </g>

  <!-- Server-side annotation -->
  <text x="735" y="52" fill="#88ccff" font-family="Roboto Mono" font-size="3.5" text-anchor="middle">Local Training</text>
  <text x="735" y="64" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5" text-anchor="middle">+</text>
  <text x="735" y="76" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5" text-anchor="middle">Privacy Controls</text>

  <!-- SuperLink node (bottom center) -->
  <g transform="translate(350,280)">
    <rect x="-100" y="-38" width="200" height="76" rx="14" fill="rgba(136,204,255,0.08)" stroke="rgba(136,204,255,0.20)" stroke-width="1"/>
    <text y="-6" text-anchor="middle" fill="#88ccff" font-family="Roboto Mono" font-size="6" font-weight="500">SuperLink</text>
    <text y="16" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="4" font-weight="500">Analyst</text>
  </g>

  <!-- Aggregation label (right of SuperLink) -->
  <text x="470" y="276" fill="#88ccff" font-family="Roboto Mono" font-size="3.5">Federated Aggregation</text>
  <text x="470" y="290" fill="#b0b8c0" font-family="Roboto Mono" font-size="2.5">Orchestrator Role</text>

  <!-- Global model broadcast UP (yellow) -->
  <path d="M335,242 C260,185 125,145 105,105" fill="none" stroke="#ffaacc" stroke-width="2.5" stroke-dasharray="8 6">
    <animate attributeName="stroke-dashoffset" from="0" to="-14" dur="0.8s" repeatCount="indefinite"/>
  </path>
  <path d="M335,242 L340,105" fill="none" stroke="#ffaacc" stroke-width="2.5" stroke-dasharray="8 6">
    <animate attributeName="stroke-dashoffset" from="0" to="-14" dur="0.8s" repeatCount="indefinite"/>
  </path>
  <path d="M335,242 C400,185 535,145 565,105" fill="none" stroke="#ffaacc" stroke-width="2.5" stroke-dasharray="8 6">
    <animate attributeName="stroke-dashoffset" from="0" to="-14" dur="0.8s" repeatCount="indefinite"/>
  </path>

  <!-- Weight updates DOWN (green) -->
  <path d="M140,105 C170,155 305,195 365,242" fill="none" stroke="#88ccff" stroke-width="2.5" stroke-dasharray="8 6">
    <animate attributeName="stroke-dashoffset" from="0" to="-14" dur="0.8s" repeatCount="indefinite"/>
  </path>
  <path d="M360,105 L365,242" fill="none" stroke="#88ccff" stroke-width="2.5" stroke-dasharray="8 6">
    <animate attributeName="stroke-dashoffset" from="0" to="-14" dur="0.8s" repeatCount="indefinite"/>
  </path>
  <path d="M600,105 C570,155 435,195 365,242" fill="none" stroke="#88ccff" stroke-width="2.5" stroke-dasharray="8 6">
    <animate attributeName="stroke-dashoffset" from="0" to="-14" dur="0.8s" repeatCount="indefinite"/>
  </path>

  <!-- Label paths (unique IDs to avoid collision with slide 2) -->
  <path id="flQL" d="M82,118 C108,160 245,200 320,258" fill="none" stroke="none"/>
  <path id="flRL" d="M122,88 C148,135 280,172 348,225" fill="none" stroke="none"/>
  <path id="flQR" d="M352,218 C420,165 552,128 578,80" fill="none" stroke="none"/>
  <path id="flRR" d="M385,252 C455,205 588,165 622,115" fill="none" stroke="none"/>

  <!-- Labels -->
  <text fill="#ffaacc" font-family="Roboto Mono" font-size="3.5" text-anchor="middle"><textPath href="#flQL" startOffset="50%">global model</textPath></text>
  <text fill="#88ccff" font-family="Roboto Mono" font-size="3.5" text-anchor="middle"><textPath href="#flRL" startOffset="50%">weight updates</textPath></text>
  <text fill="#ffaacc" font-family="Roboto Mono" font-size="3.5" text-anchor="middle"><textPath href="#flQR" startOffset="50%">global model</textPath></text>
  <text fill="#88ccff" font-family="Roboto Mono" font-size="3.5" text-anchor="middle"><textPath href="#flRR" startOffset="50%">weight updates</textPath></text>

</svg>
</div>

Model weights flow via **gRPC/TLS**. Raw data stays on each hospital's server. Only weight deltas travel.
