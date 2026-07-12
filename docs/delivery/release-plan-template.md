# Release Plan — [version, e.g. v0.2]

*Target date: · Prepared by: Project Manager Agent · Release approver: [human]*

## Release goal
What this release delivers and for whom (e.g., "stable customer demo environment").

## Contents
| Issue/PR | Title | Type | Notes |
|---|---|---|---|

## Gate status
| Gate | Status | Evidence / link | Approver |
|---|---|---|---|
| 1. Product approval | ☐ | | human |
| 2. Architecture approval | ☐ | | human |
| 3. Implementation complete | ☐ | | agent (DoD) |
| 4. QA pass | ☐ | | QA agent + human spot-check |
| 5. Security review | ☐ | | Security agent (may block) |
| 6. Cloud/FinOps review | ☐ | | FinOps agent + human for spend |
| 7. Demo/stage deployment | ☐ | | DevSecOps + human trigger |
| 8. Production approval | ☐ | | **human only** |

## Deployment plan
Environment(s), order, workflow used, config/secrets changes (approval required),
smoke tests to run.

## Rollback plan
Exact steps to return to the previous good state; who executes; how long it takes;
data considerations.

## Release notes draft
Link to Technical Writer agent's draft.

## Known issues shipping with this release
| Issue | Severity | Why acceptable |
|---|---|---|
