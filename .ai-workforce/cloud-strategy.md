# Cloud Strategy — Azure First, Google Cloud Portable

## Primary cloud: Microsoft Azure

**Why:** Azure aligns with enterprise demos, federal contractor credibility,
Microsoft-heavy customers, GitHub integration, Entra ID, Azure AI Foundry,
Azure Container Apps, Azure Static Web Apps, Azure Database for PostgreSQL,
Azure Key Vault, Application Insights, and future B2B productization.

## Secondary portability target: Google Cloud

**Why:** Google Cloud is strong for Cloud Run, Firebase, Firestore, Cloud SQL
PostgreSQL, Secret Manager, Cloud Logging, Vertex AI, Gemini, and low-cost
serverless demos. Designs must avoid Azure-only lock-in where a portable
equivalent exists at similar cost/effort.

## Default stacks

| Concern | Azure (default) | Google Cloud (equivalent) |
|---|---|---|
| Frontend | Azure Static Web Apps | Firebase Hosting or Cloud Run |
| Backend / API / agent runtime | Azure Container Apps | Cloud Run |
| Relational data | Azure Database for PostgreSQL | Cloud SQL PostgreSQL (or Firestore where doc model fits) |
| File storage | Azure Blob Storage | Cloud Storage |
| Secrets | Azure Key Vault | Secret Manager |
| Monitoring | Application Insights | Cloud Logging / Error Reporting |
| AI workloads | Azure AI Foundry / Azure OpenAI | Vertex AI / Gemini |
| CI/CD | GitHub Actions | GitHub Actions |

**Portability rules of thumb:** containerize the backend (runs on Container Apps
and Cloud Run unchanged); talk to PostgreSQL via standard drivers/ORM, not
provider-specific extensions; read secrets from environment variables so the
secret manager is swappable; keep AI-provider calls behind a thin internal interface.

## Environment model

| Env | Purpose |
|---|---|
| `local` | Developer laptop + VS Code; Docker Compose where useful |
| `dev` | Agent/human development cloud environment |
| `demo` | Stable customer demo URL — always presentable |
| `stage` | Pre-production validation; mirrors prod config |
| `prod` | Customer-ready production environment; Gate 8 protected |

Environments are separated (subscriptions/resource groups on Azure, projects on GCP).
No production data in local/dev without approval.

## Maturity model

| Version | Capability |
|---|---|
| **0.1** | Local + GitHub (code, issues, PRs, CI) |
| **0.2** | Cloud demo environment (Static Web Apps + Container Apps + PostgreSQL) |
| **0.3** | Staging, auth (Entra ID), monitoring, backups |
| **1.0** | Production SaaS foundation (multi-env, alerts, budgets, rollback, support) |

## Guardrails

- All cloud designs go through Cloud Architect (advisory) and FinOps review before
  any resource is created; humans approve provisioning (see `approval-policy.md`).
- Prefer scale-to-zero/consumption tiers per `cost-control-policy.md`.
- Deployment automation uses GitHub Actions with OIDC federation to Azure
  (no long-lived cloud credentials in GitHub secrets once configured).
