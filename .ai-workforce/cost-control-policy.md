# Cost-Control Policy

Cloud and AI spend is a first-class engineering constraint. The Cloud FinOps Analyst
agent enforces this policy; humans approve all spend.

## Rules

1. **Prefer free-tier, consumption-based, or scale-to-zero services for demos**
   (Azure Container Apps scale-to-zero, Static Web Apps free tier, Cloud Run,
   serverless PostgreSQL tiers).
2. **Estimate monthly cloud cost before adding new services.** The estimate goes in
   the issue/PR (`Cloud impact` / `Cost impact` fields). No estimate → no service.
3. **Avoid always-on compute unless justified** in writing (why scale-to-zero or
   scheduled compute won't work).
4. **Avoid expensive managed services during MVP** unless a customer requirement
   demands them — document the requirement.
5. **Track LLM token usage where practical** — log model, tokens, and cost per
   feature; prefer smaller/cheaper models where quality allows; cache and batch.
6. **Avoid excessive logging in production** — sample or filter verbose logs;
   Application Insights / Cloud Logging ingestion is a real cost.
7. **Use alerts and budgets once cloud accounts are configured** — Azure Cost
   Management budgets and GCP budget alerts on every subscription/project,
   with a hard review threshold for demo environments.
8. **The Cloud FinOps Analyst agent must review any new paid service** before a
   human approves it (Gate 6). Creating paid cloud resources without approval is
   prohibited (see `approval-policy.md`).

## Review checklist (FinOps agent)

- What does this cost at zero usage? At demo usage? At 10× demo usage?
- Is there a free-tier/serverless/consumption alternative? Why not use it?
- LLM costs: which model, expected tokens/request, requests/day, monthly estimate.
- Storage/database: tier, size, backup costs.
- Logging/monitoring: ingestion volume and retention.
- CI/CD: Actions minutes and storage within free allowance?
- What is the teardown plan if the experiment ends?
