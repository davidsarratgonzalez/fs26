## Privacy profiles

| Profile | <span class="g-term" data-g="SecAgg">SecAgg</span> | DP | Min rows | Metrics | Use case |
|---|---|---|---|---|---|
| `sandbox_open` | | | 3 | per-node | Development |
| `trusted_internal` | | | 50 | per-node | Single institution |
| `consortium_internal` | yes | | 50 | aggregate | Multi-site |
| `clinical_default` | yes | | 100 | aggregate | Hospital deployment |
| `clinical_hardened` | yes | | 200 | aggregate | High security |
| `clinical_update_noise` | yes | <span class="g-term" data-g="noise">noise</span> | 200 | aggregate | Update-level DP |
| `high_sensitivity_dp` | yes | <span class="g-term" data-g="Opacus">Opacus</span> | 500 | aggregate | Patient-level DP |

<p style="color: #c8b8a8;"><Glossary term="Trust profiles" /> are <strong>server-enforced</strong>, configured by the server administrator in the DataSHIELD settings. The analyst cannot bypass them. The <strong>most restrictive</strong> profile across all servers is adopted by all.</p>
