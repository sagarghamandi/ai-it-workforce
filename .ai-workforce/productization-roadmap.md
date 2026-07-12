# Productization Roadmap — AI IT Workforce

From local tooling to a commercial offering. Each phase builds on the previous;
phases are gated by the human owner, not by calendar.

## Phase 1: Local agent workforce in VS Code ← *current*
- Agent roles, governance, and templates defined in this repo.
- Master Orchestrator usable in Claude Code; specialist agents invocable.
- Everything runs locally; GitHub used for version control.

## Phase 2: GitHub issue and PR workflow
- Repo pushed to GitHub; issue templates and PR template live.
- Agents create issues, branches, and PRs via `gh` CLI.
- CI runs on every PR; branch protection on `main` (human merge only).

## Phase 3: Azure demo deployment
- First product MVP deployed to Azure demo environment
  (Static Web Apps + Container Apps + PostgreSQL, scale-to-zero).
- Stable demo URL; deploy via GitHub Actions with OIDC.
- FinOps budget + alerts on the demo subscription.

## Phase 4: Human approval gates and staging
- GitHub environment protection rules enforce Gate 7/8 approvals.
- Staging environment mirrors prod config; Entra ID auth; monitoring; backups.
- Release gates tracked with labels and release issues.

## Phase 5: Customer pilot readiness
- Demo scripts, pilot proposals, onboarding flows, and success criteria ready.
- Security review of the pilot surface; data-handling documented.
- Feedback collection loop wired into the backlog.

## Phase 6: Production SaaS foundation
- Production environment with rollback, alerting, budgets, and support processes.
- Billing-ready architecture (entitlements, usage tracking) — human-approved.
- Version 1.0 per the maturity model in `cloud-strategy.md`.

## Phase 7: AI Workforce Control Center dashboard
- A web dashboard showing: active agents, work in flight, gate status, approvals
  pending, cloud spend, and delivery metrics.
- Human approval actions available from the dashboard (backed by GitHub).

## Phase 8: Commercialize the AI IT Workforce as a product offering
- Package the workforce (governance + agents + workflows + control center) as a
  reusable product for other teams/customers.
- Pricing/licensing decided by humans; GTM assets from the Demo/GTM agent.
