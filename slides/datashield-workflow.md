## Classic DataSHIELD Workflow

<div style="margin-top: 0.5em;">
<svg viewBox="0 0 780 340" style="width: 100%; max-height: 390px;">

  <!-- Hospital nodes (top row) -->
  <g transform="translate(120,65)">
    <rect x="-80" y="-40" width="160" height="80" rx="14" fill="rgba(255,255,255,0.08)" stroke="rgba(255,255,255,0.15)" stroke-width="1"/>
    <rect x="-10" y="-24" width="20" height="18" rx="2" fill="none" stroke="#e0d8d0" stroke-width="1.3"/>
    <line x1="0" y1="-20" x2="0" y2="-12" stroke="#e0d8d0" stroke-width="1.3"/>
    <line x1="-4" y1="-16" x2="4" y2="-16" stroke="#e0d8d0" stroke-width="1.3"/>
    <text y="14" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="4.5" font-weight="500">Hospital A</text>
    <text y="28" text-anchor="middle" fill="#ffb366" font-family="Roboto Mono" font-size="2.8">own data</text>
  </g>

  <g transform="translate(350,65)">
    <rect x="-80" y="-40" width="160" height="80" rx="14" fill="rgba(255,255,255,0.08)" stroke="rgba(255,255,255,0.15)" stroke-width="1"/>
    <rect x="-10" y="-24" width="20" height="18" rx="2" fill="none" stroke="#e0d8d0" stroke-width="1.3"/>
    <line x1="0" y1="-20" x2="0" y2="-12" stroke="#e0d8d0" stroke-width="1.3"/>
    <line x1="-4" y1="-16" x2="4" y2="-16" stroke="#e0d8d0" stroke-width="1.3"/>
    <text y="14" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="4.5" font-weight="500">Hospital B</text>
    <text y="28" text-anchor="middle" fill="#ffb366" font-family="Roboto Mono" font-size="2.8">own data</text>
  </g>

  <g transform="translate(580,65)">
    <rect x="-80" y="-40" width="160" height="80" rx="14" fill="rgba(255,255,255,0.08)" stroke="rgba(255,255,255,0.15)" stroke-width="1"/>
    <rect x="-10" y="-24" width="20" height="18" rx="2" fill="none" stroke="#e0d8d0" stroke-width="1.3"/>
    <line x1="0" y1="-20" x2="0" y2="-12" stroke="#e0d8d0" stroke-width="1.3"/>
    <line x1="-4" y1="-16" x2="4" y2="-16" stroke="#e0d8d0" stroke-width="1.3"/>
    <text y="14" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="4.5" font-weight="500">Hospital C</text>
    <text y="28" text-anchor="middle" fill="#ffb366" font-family="Roboto Mono" font-size="2.8">own data</text>
  </g>

  <!-- Server-side annotation (right of Hospital C) -->
  <text x="720" y="52" fill="#88ccff" font-family="Roboto Mono" font-size="3.5" text-anchor="middle">Local Compute</text>
  <text x="720" y="64" fill="#88ccff" font-family="Roboto Mono" font-size="2.5" opacity="0.6" text-anchor="middle">+</text>
  <text x="720" y="76" fill="#88ccff" font-family="Roboto Mono" font-size="2.5" opacity="0.6" text-anchor="middle">Disclosure Control</text>

  <!-- Researcher node (bottom center) -->
  <g transform="translate(350,280)">
    <rect x="-100" y="-38" width="200" height="76" rx="14" fill="rgba(255,255,255,0.08)" stroke="rgba(255,255,255,0.15)" stroke-width="1"/>
    <circle cx="-16" cy="-16" r="7" fill="none" stroke="#e0d8d0" stroke-width="1.3"/>
    <path d="M-26,-4 C-26,-10 -6,-10 -6,-4" fill="none" stroke="#e0d8d0" stroke-width="1.3"/>
    <rect x="8" y="-20" width="22" height="15" rx="2" fill="none" stroke="#e0d8d0" stroke-width="1.3"/>
    <line x1="5" y1="-2" x2="33" y2="-2" stroke="#e0d8d0" stroke-width="1.3" stroke-linecap="round"/>
    <text y="26" text-anchor="middle" fill="#e0d8d0" font-family="Roboto Mono" font-size="4.5" font-weight="500">Researcher</text>
  </g>

  <!-- Result pooling label (right of researcher) -->
  <text x="470" y="276" fill="#88ccff" font-family="Roboto Mono" font-size="3.5">Result Pooling</text>
  <text x="470" y="290" fill="#88ccff" font-family="Roboto Mono" font-size="2.5" opacity="0.6">ds.glm() · ds.mean() · ds.var()</text>

  <!-- Query paths (researcher → hospitals) -->
  <path id="qA" d="M335,242 C260,185 125,145 105,105" fill="none"/>
  <path id="qB" d="M335,242 L340,105" fill="none"/>
  <path id="qC" d="M335,242 C400,185 535,145 565,105" fill="none"/>

  <!-- Result paths (hospitals → researcher) -->
  <path id="rA" d="M140,105 C170,155 305,195 365,242" fill="none"/>
  <path id="rB" d="M360,105 L365,242" fill="none"/>
  <path id="rC" d="M600,105 C570,155 435,195 365,242" fill="none"/>

  <!-- Queries flowing UP (yellow) -->
  <use href="#qA" class="flow-query"/>
  <use href="#qB" class="flow-query"/>
  <use href="#qC" class="flow-query"/>

  <!-- Results flowing DOWN (green) -->
  <use href="#rA" class="flow-result"/>
  <use href="#rB" class="flow-result"/>
  <use href="#rC" class="flow-result"/>

  <!-- Label paths -->
  <path id="lblQL" d="M82,118 C108,160 245,200 320,258" fill="none" stroke="none"/>
  <path id="lblRL" d="M122,88 C148,135 280,172 348,225" fill="none" stroke="none"/>
  <path id="lblQR" d="M352,218 C420,165 552,128 578,80" fill="none" stroke="none"/>
  <path id="lblRR" d="M385,252 C455,205 588,165 622,115" fill="none" stroke="none"/>

  <!-- Labels -->
  <text fill="#FFD000" font-family="Roboto Mono" font-size="3.5" text-anchor="middle"><textPath href="#lblQL" startOffset="50%">queries</textPath></text>
  <text fill="#66ddaa" font-family="Roboto Mono" font-size="2.8" text-anchor="middle"><textPath href="#lblRL" startOffset="50%">aggregated results</textPath></text>
  <text fill="#FFD000" font-family="Roboto Mono" font-size="3.5" text-anchor="middle"><textPath href="#lblQR" startOffset="50%">queries</textPath></text>
  <text fill="#66ddaa" font-family="Roboto Mono" font-size="2.8" text-anchor="middle"><textPath href="#lblRR" startOffset="50%">aggregated results</textPath></text>

</svg>
</div>

Data **never leaves** the hospital. Each server computes locally. Non-disclosive summaries return to the analyst, where DataSHIELD pools them automatically.
