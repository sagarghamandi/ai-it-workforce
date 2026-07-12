# AI IT Workforce

A practical, human-in-the-loop, semi-autonomous **AI software delivery team** that runs
inside VS Code + Claude Code, uses **GitHub as the system of record**, and deploys to
**Azure first** with **Google Cloud portability**.

This repo is not an application — it is the **operating system for an AI-assisted IT
delivery team** used to build real products and MVPs.

## What's in this repo

| Path | Purpose |
|---|---|
| `CLAUDE.md` | How Claude behaves here (rules, defaults, hard limits) |
| `.ai-workforce/` | Governance: registry, approval policy, execution modes, cloud strategy, cost & security policy, release gates, roadmap |
| `.claude/agents/` | Role prompts for 17 specialist agents |
| `docs/` | Architecture docs and product/delivery/demo templates |
| `.github/` | Issue templates, PR template, CI and demo-deploy workflows |

## How the AI workforce works

1. **You chat with the Master Orchestrator** — describe a business goal, product idea,
   or problem in plain language.
2. The orchestrator classifies the request, selects specialist agents (Product Owner,
   Solution Architect, Full Stack Developer, QA, DevSecOps, FinOps, etc.), and produces
   a delivery plan: GitHub issues, acceptance criteria, approval gates, risks, and
   cloud/cost/security impact.
3. Specialist agents execute approved work: they draft PRDs, design architecture,
   write code on **feature branches**, add tests and docs, and **open Pull Requests**.
4. **Humans review and merge.** Agents never merge to `main`, never deploy to
   production, and never touch secrets, auth, billing, or customer communications
   without explicit approval.

## How humans stay in the loop

Three execution modes (`.ai-workforce/human-in-the-loop.md`):

- **Advisory** — agents recommend only (strategy, architecture, cost, security, legal, customer-facing).
- **Assisted execution** — agents edit files and open PRs; humans review before merge.
- **Autonomous low-risk** — docs cleanup, formatting, test generation, issue drafting,
  lint fixes, local refactors. Never production changes.

The full approval matrix is in `.ai-workforce/approval-policy.md`, and eight release
gates (product → architecture → implementation → QA → security → FinOps → demo/stage →
production approval) are in `.ai-workforce/release-gates.md`.

## Using the Master Orchestrator

Open this repo in VS Code, start Claude Code, and say something like:

> "I want to build an MVP for [idea]. Target customers are [X]. I want a demo in 3 weeks."

The orchestrator responds in a fixed format: intent, request type, agents involved,
execution mode, delivery plan, GitHub issues to create, acceptance criteria, human
approval gates, risks, cloud/cost/security impact, and a suggested next action.
You approve, redirect, or override — then work begins.

## How work flows through GitHub

- **Issues** are the backlog — created from templates in `.github/ISSUE_TEMPLATE/`
  with agent role, approval requirements, and acceptance criteria built in.
- **Branches** — one feature branch per issue.
- **Pull Requests** — the review and approval mechanism, using the PR template's
  security/cloud/cost/approval checklist.
- **GitHub Actions** — CI on every PR (`.github/workflows/ci.yml`); demo deployment
  is a placeholder until Azure is configured (`deploy-demo-placeholder.yml`).

## Cloud deployment

**Azure-first**: Static Web Apps (frontend), Container Apps (backend/agents),
Azure Database for PostgreSQL, Blob Storage, Key Vault, Application Insights,
Azure AI Foundry / Azure OpenAI — deployed via GitHub Actions.

**Google Cloud portable**: Cloud Run, Cloud SQL PostgreSQL, Cloud Storage,
Secret Manager, Vertex AI / Gemini as the mapped equivalents.

Environments: `local → dev → demo → stage → prod`, with cost controls
(free-tier / scale-to-zero preferred) enforced by the Cloud FinOps Analyst agent.
Details: `.ai-workforce/cloud-strategy.md`.
