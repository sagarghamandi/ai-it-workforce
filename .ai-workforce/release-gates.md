# Release Gates

Eight sequential gates between an idea and production. Gates 1, 2, and 8 are always
human decisions. Gates 3–7 are agent-verified and human-spot-checked. A release may
not skip a gate; a gate may only be waived by an explicit, documented human decision.

| # | Gate | Owner (agent) | Approver | Pass criteria |
|---|------|---------------|----------|---------------|
| 1 | **Product approval** | Product Owner agent | Human product owner | PRD/scope approved; MVP boundary set; demo value clear |
| 2 | **Architecture approval** | Solution + Cloud Architect | Human architect/owner | Design + ADRs reviewed; API/data contracts set; no unresolved major concerns |
| 3 | **Implementation complete** | Developer/Data/AI-ML agents | — (self-certified vs. DoD) | All issue acceptance criteria met; DoD items 1–5 satisfied; PR open |
| 4 | **QA pass** | QA/Test Engineer | Human (spot-check) | All test levels green; acceptance criteria verified; no open critical/major bugs |
| 5 | **Security review** | Security & Compliance | Human for exceptions | Threat model current; no critical findings; secrets/auth/privacy clean. **Security may block here.** |
| 6 | **Cloud/FinOps review** | Cloud FinOps Analyst | Human for spend | Cost estimated; no unapproved paid services; within budget policy |
| 7 | **Demo/stage deployment** | DevSecOps Engineer | Human triggers deploy | Deploys cleanly to demo/stage; smoke tests pass; rollback plan documented |
| 8 | **Production approval** | — | **Human only** | Explicit human sign-off; GitHub environment protection satisfied; rollback verified |

## Rules

- **Gate 5 block:** if the Security & Compliance agent identifies a critical risk,
  the release is blocked regardless of other gates. Only a human-approved,
  documented security exception unblocks it.
- **Gate 8 is never delegated.** No agent may approve, trigger, or "helpfully
  complete" a production deployment.
- Gate status is tracked on the release issue with labels
  (`gate:1-passed` … `gate:8-pending`).
- A failed gate sends work back to the responsible agent with findings recorded
  in the issue — not quietly patched around.
