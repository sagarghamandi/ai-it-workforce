# Definition of Done

A task is **done** only when every applicable item below is true. Agents must not
close issues, request final review, or report completion while any applicable item
is unmet. "Not applicable" is fine — but must be stated, not silently skipped.

## Checklist

1. **Requirement is clearly understood** — restated in the issue in the agent's own words.
2. **Acceptance criteria are defined** — testable, written in the issue before implementation.
3. **Implementation is completed in a feature branch** — never directly on `main`.
4. **Tests are added or updated** — covering the new behavior and edge cases.
5. **Existing tests pass** — full suite, locally and in CI.
6. **Security-sensitive changes are reviewed** — auth, secrets, input handling, data
   exposure trigger a Security & Compliance review (Gate 5).
7. **Cloud/cost impact is considered** — new services or usage growth trigger a
   FinOps review (Gate 6); "no cloud impact" is an acceptable, explicit answer.
8. **Documentation is updated** — README, API docs, deployment guide, whichever apply.
9. **PR is created** — using the PR template, linked to the issue, agent role identified.
10. **Human review is complete where required** — per `approval-policy.md`.
11. **Demo/stage deployment passes where applicable** — the change works in a deployed
    environment, not just locally.
12. **Release notes are updated where applicable** — user-visible changes are recorded.

## Anti-patterns that mean "not done"

- "Works on my machine" with no tests.
- Tests weakened, skipped, or deleted to get green CI.
- Docs describing the old behavior.
- PR opened without linked issue or acceptance criteria.
- Approval-required change bundled inside an innocent-looking PR.
