## Privacy profiles

| Profile | SecAgg | DP | Min rows | Metrics | Use case |
|---|---|---|---|---|---|
| `sandbox_open` | | | 3 | per-node | Development |
| `trusted_internal` | | | 50 | per-node | Single institution |
| `consortium_internal` | yes | | 50 | aggregate | Multi-site |
| `clinical_default` | yes | | 100 | aggregate | Hospital deployment |
| `clinical_hardened` | yes | | 200 | aggregate | High security |
| `clinical_update_noise` | yes | noise | 200 | aggregate | Update-level DP |
| `high_sensitivity_dp` | yes | Opacus | 500 | aggregate | Patient-level DP |

<Glossary term="Trust profiles" /> are **server-enforced**, configured by the server administrator in the DataSHIELD settings. The analyst cannot bypass them. The **most restrictive** profile across all servers is adopted by all.
