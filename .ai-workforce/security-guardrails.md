# Security Guardrails

Baseline security rules for all agents and humans in this ecosystem. The Security &
Compliance Engineer agent enforces them and **may block any release** (Gate 5).

## Rules

1. **Never commit secrets.** No API keys, passwords, tokens, or connection strings in
   code, config, issues, PRs, or docs. `.gitignore` covers `.env*`; that is a backstop,
   not a strategy.
2. **Use environment variables and secret managers** — Azure Key Vault (primary),
   GCP Secret Manager (portability). Local dev uses `.env` files that are never committed;
   provide `.env.example` with placeholder values.
3. **Validate inputs** — all external input (API requests, file uploads, LLM outputs
   used as instructions or queries) is untrusted. Validate, constrain, parameterize.
4. **Use least privilege** — minimal scopes for tokens, cloud identities, and database
   roles; GitHub Actions use OIDC federation, not long-lived credentials, once configured.
5. **Separate dev/demo/stage/prod** — distinct resource groups/projects, identities,
   and secrets per environment.
6. **Do not use production data in local/dev without approval** — prefer synthetic or
   anonymized data.
7. **Add dependency scanning where practical** — enable Dependabot/`npm audit`/
   `pip-audit` in CI; review new dependencies for maintenance health and license.
8. **Keep authentication and authorization changes under human review** — always
   approval-required, never autonomous (see `approval-policy.md`).
9. **Document risks and mitigations** — security-relevant decisions get a short
   written risk note in the issue/ADR; accepted risks are explicit, not silent.
10. **The Security Agent may block release** — a critical finding at Gate 5 stops the
    release until fixed or a human approves a documented exception.

## Security review triggers

A Security & Compliance review is mandatory when a change touches: authentication or
authorization; secrets or key handling; personally identifiable or customer data;
file upload/parsing; new external dependencies or APIs; infrastructure or network
exposure; LLM prompts that process untrusted content (prompt injection surface).

## AI-specific guardrails

- Treat LLM output as untrusted input to downstream systems.
- Never place secrets or customer PII in prompts sent to external model APIs
  without approval and a documented data-handling basis.
- Log AI actions that modify state, so they are auditable.
