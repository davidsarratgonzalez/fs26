## Privacy model

Four layers of protection against an untrusted researcher:

<div class="grid grid-cols-2 gap-6 mt-4">
<div>

### Layer 1:DataSHIELD
Raw data stays on the server. The researcher only calls approved methods.

### Layer 2:SecAgg+
Individual weight updates are encrypted. The researcher only sees the **aggregate**.

</div>
<div>

### Layer 3:DP-SGD
Each node adds calibrated noise before sending. Formal guarantees via Opacus.

### Layer 4:Disclosure control
Bucketed counts, suppressed per-node metrics, minimum sample sizes.

</div>
</div>
