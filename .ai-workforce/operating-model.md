# Operating Model — How the AI IT Workforce Delivers

## Principles

1. **VS Code is the development cockpit** — humans and agents work here.
2. **GitHub is the system of record** — if it isn't in GitHub, it didn't happen.
3. **GitHub Issues are the backlog** — every unit of work is an issue with an agent role, acceptance criteria, and approval flags.
4. **Pull Requests are the review and approval mechanism** — agents open PRs; humans merge.
5. **GitHub Actions are the CI/CD mechanism.**
6. **Azure is the primary demo/productization cloud; Google Cloud is the portability target.**
7. **Agents may create** plans, issues, branches, code, tests, docs, and deployment workflows.
8. **Agents must not**, without explicit human approval: merge to main, deploy to production, delete data, modify secrets, alter authentication, change billing/payment logic, or send customer communications.
9. **Both human-led and agent-assisted execution are supported** — a human can pick up any issue an agent would have done, and vice versa.
10. **This is augmentation, not replacement** — humans can intervene, review, approve, override, or redirect at any time.

## Standard delivery flow

```
Business intent (human ↔ Master Orchestrator)
      │
      ▼
Plan: request type, agents, execution mode, risks, approvals   [Gate 1: Product approval]
      │
      ▼
GitHub Issues created (templates in .github/ISSUE_TEMPLATE/)
      │
      ▼
Design: Solution Architect + Cloud Architect + UX             [Gate 2: Architecture approval]
      │
      ▼
Build: Developer/Data/AI-ML agents on feature branches        [Gate 3: Implementation complete]
      │
      ▼
Verify: QA tests + acceptance criteria                        [Gate 4: QA pass]
      │
      ▼
Review: Security & Compliance                                 [Gate 5: Security review]
        Cloud FinOps                                          [Gate 6: FinOps review]
      │
      ▼
PR review → human merge → demo/stage deploy                   [Gate 7: Demo/stage deployment]
      │
      ▼
Production                                                    [Gate 8: Human approval for production]
```

## Roles of the humans

- **Product owner (you):** approves scope, priorities, monetization, customer-facing anything.
- **Architect/reviewer:** approves architecture, schema, auth, infra changes.
- **Release approver:** merges PRs, approves stage/prod deployments.
- Any human may **stop, override, or redirect** any agent at any time; agents must comply immediately and record the redirect in the relevant issue.

## Conventions

- Every artifact names its acting agent role, e.g. `[QA/Test Engineer]`.
- Branch naming: `feat/<issue#>-<slug>`, `fix/<issue#>-<slug>`, `docs/<issue#>-<slug>`.
- One issue → one branch → one PR, whenever practical.
- Issues carry labels for role (`agent:developer`), mode (`mode:assisted`), and gate status (`gate:security-pending`).
- Progress summaries are written for business readers first, engineers second.

## Related policies

- Execution modes: `human-in-the-loop.md`
- Approval matrix: `approval-policy.md`
- Done criteria: `definition-of-done.md`
- Gates: `release-gates.md`
- Cloud: `cloud-strategy.md` · Cost: `cost-control-policy.md` · Security: `security-guardrails.md`
