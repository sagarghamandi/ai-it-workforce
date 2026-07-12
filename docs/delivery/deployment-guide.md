# Deployment Guide

How products built by this workforce are deployed. This guide starts as the
process skeleton; the DevSecOps Engineer agent and Technical Writer agent fill in
product-specific commands as products come to exist.

## Principles

- Deployments are **scripted and repeatable** (GitHub Actions), never hand-rolled.
- **Humans trigger** demo/stage/prod deployments; agents may deploy to local/dev only.
- Every deployment has a **rollback plan before it runs**.
- Secrets come from Key Vault / Secret Manager via environment configuration —
  never from the repo.

## Environments

| Env | Where | Deploy trigger | Approval |
|---|---|---|---|
| local | laptop / Docker Compose | developer/agent | none |
| dev | Azure dev resource group | agent or human, on merge to a dev branch | none |
| demo | Azure demo resource group | human-triggered workflow | Gate 7 |
| stage | Azure stage resource group | human-triggered workflow | Gate 7 |
| prod | Azure prod resource group | human-triggered, environment-protected workflow | **Gate 8, human only** |

## Standard flow

1. PR merged to `main` by a human (CI green, reviews done).
2. Release plan gate checklist complete (`release-plan-template.md`).
3. Human triggers the deploy workflow for the target environment
   (see `.github/workflows/deploy-demo-placeholder.yml` until real workflows exist).
4. Smoke tests run post-deploy; results recorded on the release issue.
5. On failure: execute the rollback plan; file an incident issue.

## Azure setup prerequisites (one-time, human-performed)

- [ ] Azure subscription + resource groups per environment
- [ ] Entra ID app registration for GitHub OIDC federation (no stored cloud secrets)
- [ ] Key Vault per environment, populated by a human
- [ ] Budget + alerts per subscription (FinOps)
- [ ] GitHub environments (`demo`, `stage`, `prod`) with required reviewers

## Rollback

Default rollback = redeploy the previous known-good image/tag. Product-specific
steps (data migrations!) are documented in each release plan. Schema migrations
require their own tested down-path or restore plan **before** deploy approval.

## Per-product sections (append as products are created)

*(none yet)*
