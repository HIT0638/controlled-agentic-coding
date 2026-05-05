---
description: Prompt template for surfacing the highest-value hidden assumptions, failure modes, and unknown unknowns for a scoped coding task.
metadata:
  tags: [delegation, risk-map, failure-modes, verification]
---

Use the Controlled Agentic Coding Workflow Skill and the AI Delegation Risk Add-on.

Workflow mode: inherit current mode
Add-on: risk-map
Default level: inherit the current workflow mode. Do not escalate side effects.

Task:
[TASK]

Artifact:
[FILE / MODULE / API / PIPELINE / CONFIG / DIFF]

Goal:
Identify the top 5-10 highest-value risks worth planning or verifying.

Rules:
- Tailor the risk set to artifact type and codebase position.
- Do not produce a generic checklist.
- Prefer production-facing failure modes over style or taste issues.
- Separate confirmed, inferred, and unknown evidence levels.
- Acknowledge unknown unknowns when interfaces, callers, or failure signals are incomplete.
- Every listed risk must include a concrete minimal check, or explicitly state why no reliable check is currently known.

Output:
## Artifact type

## Assumptions
List the assumptions the current plan or implementation appears to rely on.

## Selected risk categories
Only include categories that materially apply here.

## High-risk unknown unknowns
Name the areas where missing context could hide important failure.

## Risk Table
| Risk | Hidden assumption | Why it matters | How it appears | Verification abstraction | Minimal check | Severity | Evidence level |
| --- | --- | --- | --- | --- | --- | --- | --- |

## Verification implications
Explain what kinds of checks would actually reduce confidence risk here.

## Questions before trusting this
List the smallest unanswered questions that still matter.

## Recommended next workflow step
Choose one:
- stay in Task Recon
- move to Plan Change
- require human design review first
- defer implementation

Exit criteria:
- The list stays focused on the top risks.
- Each risk ties to a concrete assumption or failure mode.
- Verification implications are specific enough to affect planning.
