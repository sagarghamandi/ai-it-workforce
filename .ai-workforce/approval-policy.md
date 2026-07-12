# Approval Policy — What Agents May Do, and When Humans Must Decide

This is the canonical approval matrix. When a task spans categories, the strictest
applicable rule wins. When in doubt: ask.

## ✅ Agents may do autonomously

- Draft PRDs
- Draft user stories
- Create backlog items
- Create GitHub issues
- Write documentation
- Add test cases
- Fix linting
- Refactor small internal code (no behavior or interface changes)
- Create feature branches
- Open pull requests
- Deploy to local/dev environment
- Prepare demo deployment scripts (prepare — not execute against cloud)

## 🟡 Human approval required (before the action)

- Merge to `main`
- Production deployment
- Database schema migration
- Authentication or authorization changes
- Billing/payment changes
- Customer-facing communication (email, docs, proposals, demos delivered to customers)
- Creating paid cloud services
- Modifying secrets
- Deleting files or data
- Changing infrastructure significantly (topology, regions, networking, environments)
- Legal/IP/licensing decisions (including adding dependencies with restrictive licenses)
- Security exception approval

**How to request approval:** the agent states clearly — in chat and in the relevant
issue/PR — what it wants to do, why, the risk, the cost impact, and the rollback plan,
then stops until a human answers.

## ⛔ Strictly prohibited (no approval path in normal operation)

These require a deliberate, documented human decision outside normal workflow —
an agent must never do them and never treat routine assent as authorization:

- Hardcoding credentials
- Committing API keys or secrets
- Deleting databases
- Sending emails to customers
- Deploying to production (agents never execute this; humans do, or humans trigger
  an approved pipeline with GitHub environment protection)
- Exposing private data
- Creating expensive cloud resources
- Changing DNS records
- Disabling tests or security checks to force a release

## Enforcement

- The PR template carries a human approval checklist; reviewers verify it.
- GitHub environment protection rules (once configured) enforce deploy approvals.
- The Security & Compliance agent may **block** any release (see `release-gates.md`).
- Violations are treated as incidents: stop work, document in an issue, review the
  guardrail that failed.
