# AI Workforce Architecture

How the AI IT Workforce itself is structured and operates.

## Layers

```
┌─────────────────────────────────────────────────────────┐
│ HUMANS: product owner, architects, reviewers, approvers │
│   intervene / review / approve / override / redirect    │
├─────────────────────────────────────────────────────────┤
│ MASTER ORCHESTRATOR (chat interface in Claude Code)     │
│   intent → classification → plan → issues → delegation  │
├─────────────────────────────────────────────────────────┤
│ SPECIALIST AGENTS (.claude/agents/)                     │
│   Product │ PM │ Scrum │ Arch │ Cloud │ UX │ Dev        │
│   Data │ AI/ML │ QA │ DevSecOps │ Security │ Writer     │
│   FinOps │ Demo/GTM │ Customer Success                  │
├─────────────────────────────────────────────────────────┤
│ GOVERNANCE (.ai-workforce/)                             │
│   registry · modes · approvals · DoD · gates ·          │
│   cloud/cost/security policy                            │
├─────────────────────────────────────────────────────────┤
│ SYSTEM OF RECORD (GitHub)                               │
│   Issues (backlog) · Branches · PRs (approval) ·        │
│   Actions (CI/CD) · Environments (deploy protection)    │
├─────────────────────────────────────────────────────────┤
│ RUNTIME TARGETS                                         │
│   local (VS Code/Docker) → Azure dev/demo/stage/prod    │
│   (Google Cloud portable)                               │
└─────────────────────────────────────────────────────────┘
```

## Control flow

1. Human states intent to the **Master Orchestrator**.
2. Orchestrator produces a plan in its fixed output format (agents, mode, issues,
   acceptance criteria, gates, risks, cloud/cost/security impact).
3. Human approves/edits the plan → issues are created from templates.
4. Specialist agents execute per their registry entry
   (`.ai-workforce/agent-registry.yaml`) and declared mode.
5. Work flows through the 8 release gates; humans hold Gates 1, 2, and 8, plus all
   approval-matrix items.
6. PRs are the merge point of agent work and human judgment.

## Trust model

- Agents are constrained by: (a) their role prompt, (b) the registry, (c) the
  approval policy, (d) GitHub branch/environment protection (mechanical enforcement
  once configured).
- Prompt-level rules are advisory-by-construction; **mechanical enforcement lives in
  GitHub** (branch protection, required reviews, environment approvals) and should be
  configured as soon as the repo is pushed (Phase 2 of the roadmap).

## Extension points

- New agent = new file in `.claude/agents/` + registry entry + (optionally) issue template.
- New product built by this workforce lives in its own repo (or `/products/<name>`
  subfolder if a monorepo is preferred), inheriting this governance via its own
  CLAUDE.md pointer.
