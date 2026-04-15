## Ecosystem

<div class="grid grid-cols-2 gap-8 mt-4">
<div>

### Server (each hospital)
| Package | Role |
|---|---|
| **dsFlower** | FL orchestration, privacy |
| **dsImaging** | Medical imaging (S3/MinIO) |
| **dsRadiomics** | Feature extraction |
| **dsJobs** | Durable job runtime |

</div>
<div>

### Client (researcher)
| Package | Role |
|---|---|
| **dsFlowerClient** | Recipes, training API |
| **dsImagingClient** | Dataset discovery |
| **dsRadiomicsClient** | Extraction workflows |
| **dsJobsClient** | Job monitoring |

</div>
</div>
