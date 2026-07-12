# Cloud Architecture — Google Cloud (Portability Target)

The Google Cloud equivalent of the Azure reference architecture. Maintained so any
product can be redeployed to GCP with bounded effort. See
`docs/architecture/cloud-architecture-azure.md` for the primary design.

## Service mapping

| Concern | Azure (primary) | GCP (portable) | Portability notes |
|---|---|---|---|
| Frontend | Static Web Apps | Firebase Hosting or Cloud Run | Static assets port trivially |
| Backend/API/agents | Container Apps | **Cloud Run** | Same container image runs on both — keep it containerized |
| Database | Azure PostgreSQL Flexible | **Cloud SQL PostgreSQL** (or Firestore if doc model fits) | Standard drivers/ORM only; no provider-specific extensions |
| Files | Blob Storage | Cloud Storage | Abstract behind a storage interface or S3-compatible layer |
| Secrets | Key Vault | Secret Manager | Apps read env vars; injection layer differs, code doesn't |
| Monitoring | Application Insights | Cloud Logging / Error Reporting | Use OpenTelemetry to stay neutral where practical |
| AI | Azure OpenAI / AI Foundry | Vertex AI / Gemini | Keep model calls behind a thin internal interface |
| Identity | Entra ID | Identity Platform / Google Identity | Use OIDC standards; avoid provider-specific claims |
| CI/CD | GitHub Actions | GitHub Actions (same) | Swap deploy steps + OIDC (Workload Identity Federation) |

## Reference architecture (GCP demo tier)

```
Users ──► Firebase Hosting ──► Cloud Run (scale-to-zero)
                                  │        │        │
                       Cloud SQL PG   Cloud Storage  Vertex AI/Gemini
                                  │
                       Secret Manager · Cloud Logging
          CI/CD: GitHub Actions ──WIF/OIDC──► GCP
```

## Portability rules (enforced at design time)

1. **Containerize the backend** — the same image must run on Container Apps and Cloud Run.
2. **PostgreSQL via standard drivers/ORM** — no cloud-proprietary DB features without an ADR.
3. **Secrets via environment variables** — the app never knows which secret manager it's behind.
4. **AI calls behind an internal interface** — swapping Azure OpenAI ↔ Vertex is one adapter.
5. **Infrastructure differences live in IaC and CI**, not application code.

## Migration checklist (Azure → GCP)

- [ ] Build/push image to Artifact Registry; deploy to Cloud Run
- [ ] Provision Cloud SQL PostgreSQL; run schema migrations; migrate data (pg_dump/restore)
- [ ] Recreate secrets in Secret Manager; wire env vars
- [ ] Point frontend hosting at Firebase Hosting or Cloud Run
- [ ] Swap GitHub Actions deploy jobs to WIF/OIDC + gcloud steps
- [ ] Re-run smoke tests and the QA gate against the GCP environment
