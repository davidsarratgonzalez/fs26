## How it works

<div class="grid grid-cols-3 gap-6 mt-8">
<div class="step-card" style="text-align: center;">
  <div style="font-family: 'Roboto Mono'; font-size: 1.6em; color: #FFD000;">1</div>
  <div style="font-family: 'Roboto Mono'; font-size: 0.8em; text-transform: uppercase; color: #f0e8e0; letter-spacing: 0.05em;">Connect</div>
  <div style="font-size: 0.8em; color: #a89888; margin-top: 0.4em;">Researcher connects to N hospital nodes via DataSHIELD</div>
</div>
<div class="step-card" style="text-align: center;">
  <div style="font-family: 'Roboto Mono'; font-size: 1.6em; color: #FFD000;">2</div>
  <div style="font-family: 'Roboto Mono'; font-size: 0.8em; text-transform: uppercase; color: #f0e8e0; letter-spacing: 0.05em;">Train</div>
  <div style="font-size: 0.8em; color: #a89888; margin-top: 0.4em;">Each node trains on local data, sends weight updates to SuperLink</div>
</div>
<div class="step-card" style="text-align: center;">
  <div style="font-family: 'Roboto Mono'; font-size: 1.6em; color: #FFD000;">3</div>
  <div style="font-family: 'Roboto Mono'; font-size: 0.8em; text-transform: uppercase; color: #f0e8e0; letter-spacing: 0.05em;">Aggregate</div>
  <div style="font-size: 0.8em; color: #a89888; margin-top: 0.4em;">SuperLink averages updates, sends global model back. Repeat N rounds.</div>
</div>
</div>
