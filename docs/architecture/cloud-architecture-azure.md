# Cloud Architecture — Azure (Primary)

Default Azure architecture for products built by this workforce. Instantiate and
tailor per product; keep cost annotations current. See `.ai-workforce/cloud-strategy.md`
for strategy and `.ai-workforce/cost-control-policy.md` for cost rules.

## Reference architecture (demo/MVP tier)

```
                 ┌──────────────────────────────┐
   Users ──────► │ Azure Static Web Apps        │  frontend (free tier)
                 └──────────────┬───────────────┘
                                │ HTTPS
                 ┌──────────────▼───────────────┐
                 │ Azure Container Apps         │  backend / API / agent runtime
                 │ (scale-to-zero, consumption) │
                 └───┬──────────┬───────────┬───┘
                     │          │           │
     ┌───────────────▼──┐  ┌────▼───────┐  ┌▼──────────────────┐
     │ Azure Database   │  │ Azure Blob │  │ Azure OpenAI /    │
     │ for PostgreSQL   │  │ Storage    │  │ AI Foundry        │
     │ (Flexible, B1ms) │  │            │  │ (future AI load)  │
     └──────────────────┘  └────────────┘  └───────────────────┘
                     │
     ┌───────────────▼──────────────┐   ┌───────────────────────┐
     │ Azure Key Vault (secrets)    │   │ Application Insights  │
     └──────────────────────────────┘   │ (sampled telemetry)   │
                                        └───────────────────────┘

     CI/CD: GitHub Actions ──OIDC──► Azure (no stored credentials)
```

## Service choices

| Concern | Service | Tier guidance (MVP/demo) |
|---|---|---|
| Frontend | Static Web Apps | Free tier |
| Backend/API/agents | Container Apps | Consumption, scale-to-zero, min replicas 0 |
| Database | Azure Database for PostgreSQL Flexible Server | Burstable B1ms; stop when idle in dev |
| Files | Blob Storage | Standard LRS, hot |
| Secrets | Key Vault | Standard |
| Monitoring | Application Insights | Sampling on; short retention for demo |
| AI | Azure OpenAI / AI Foundry | Consumption; FinOps-reviewed model choice |
| Identity (v0.3+) | Entra ID | Free/P1 as needed |
| CI/CD | GitHub Actions + OIDC federation | Free minutes budget |

## Environments

One resource group per environment: `rg-<product>-dev`, `-demo`, `-stage`, `-prod`.
Separate Key Vaults and identities per environment. Prod gets: backups enabled,
budget alerts, environment-protected deployments (Gate 8).

## To fill in per product

- [ ] Product name and resource naming convention
- [ ] Region (default: closest low-cost region to demo audience)
- [ ] Monthly cost estimate per environment (FinOps, Gate 6)
- [ ] Data classification and backup/retention needs
- [ ] IaC location (Bicep/Terraform) once created
