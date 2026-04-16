## Privacy Model

Four layers of protection against the analyst:

<div style="display: flex; flex-direction: column; gap: 12px; margin-top: 1.2em;">

<div v-click style="background: rgba(102,221,170,0.10); border: 1px solid rgba(102,221,170,0.15); border-radius: 10px; padding: 0.7em 1.2em;">
  <div style="display: flex; align-items: baseline; gap: 14px; margin-bottom: 4px;">
    <span style="font-family: 'Roboto Mono', monospace; color: #66ddaa; font-weight: 600; font-size: 1.1em;">Layer 1</span>
    <span style="color: #e0d8d0; font-weight: 500;">DataSHIELD</span>
  </div>
  <div style="color: #b8b0a8; font-size: 0.9em;">Raw data stays on the server. The researcher only calls approved methods.</div>
</div>

<div v-click style="background: rgba(102,221,170,0.10); border: 1px solid rgba(102,221,170,0.15); border-radius: 10px; padding: 0.7em 1.2em;">
  <div style="display: flex; align-items: baseline; gap: 14px; margin-bottom: 4px;">
    <span style="font-family: 'Roboto Mono', monospace; color: #66ddaa; font-weight: 600; font-size: 1.1em;">Layer 2</span>
    <span style="color: #e0d8d0; font-weight: 500;"><Glossary term="SecAgg+" /></span>
  </div>
  <div style="color: #b8b0a8; font-size: 0.9em;">Individual weight updates are encrypted. The researcher only sees the <strong>aggregate</strong>.</div>
</div>

<div v-click style="background: rgba(102,221,170,0.10); border: 1px solid rgba(102,221,170,0.15); border-radius: 10px; padding: 0.7em 1.2em;">
  <div style="display: flex; align-items: baseline; gap: 14px; margin-bottom: 4px;">
    <span style="font-family: 'Roboto Mono', monospace; color: #66ddaa; font-weight: 600; font-size: 1.1em;">Layer 3</span>
    <span style="color: #e0d8d0; font-weight: 500;"><Glossary term="DP-SGD" /></span>
  </div>
  <div style="color: #b8b0a8; font-size: 0.9em;">Each node adds calibrated noise before sending. Formal guarantees via Opacus.</div>
</div>

<div v-click style="background: rgba(102,221,170,0.10); border: 1px solid rgba(102,221,170,0.15); border-radius: 10px; padding: 0.7em 1.2em;">
  <div style="display: flex; align-items: baseline; gap: 14px; margin-bottom: 4px;">
    <span style="font-family: 'Roboto Mono', monospace; color: #66ddaa; font-weight: 600; font-size: 1.1em;">Layer 4</span>
    <span style="color: #e0d8d0; font-weight: 500;"><Glossary term="Disclosure control" /></span>
  </div>
  <div style="color: #b8b0a8; font-size: 0.9em;">Bucketed counts, suppressed per-node metrics, minimum sample sizes.</div>
</div>

</div>
