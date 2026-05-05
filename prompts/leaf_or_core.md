---
description: Prompt template for classifying whether a task touches leaf code, architecture-sensitive core code, or a mixed boundary.
metadata:
  tags: [delegation, risk, codebase-position, architecture]
---

Use the Controlled Agentic Coding Workflow Skill and the AI Delegation Risk Add-on.

Workflow mode: inherit current mode
Add-on: leaf-or-core
Default level: inherit the current workflow mode. Do not escalate side effects.

Task:
[TASK]

Scope:
[FILES / MODULES / DIFF / ARTIFACT]

Goal:
Judge whether the touched area is leaf, core, mixed, or still unknown.

Rules:
- Do not treat this as edit approval.
- Do not treat this as command approval.
- Classify conservatively when evidence is weak.
- Prefer `mixed` or `core` when a leaf-looking task touches architecture-sensitive surfaces.
- Stop once the classification, blast radius, and next inspection targets are clear enough.

Mixed/core-sensitive triggers include:

- shared or public APIs
- schemas or data contracts
- auth or permission logic
- global config
- reusable abstractions
- migration logic
- transaction boundaries
- concurrency boundaries
- high-reuse utilities

Output:
## Classification
Choose one: `leaf`, `core`, `mixed`, `unknown`

## Evidence
Separate confirmed facts from inference.

## Downstream dependents / blast radius
If known, name who depends on this area and how far failure may propagate.

## Public interfaces and architecture-sensitive surfaces
List touched or likely touched APIs, schemas, dependency surfaces, contracts, or global behaviors.

## Technical debt propagation risk
Explain whether local shortcuts would stay local or spread into shared code paths later.

## AI freedom judgment
Choose one:
- AI may implement freely within scoped leaf boundaries
- AI may implement only under a strict human plan and review
- AI should only assist human-owned design

## Questions / next inspection targets
Name the smallest next slice that would most reduce uncertainty.

Exit criteria:
- Classification is explicit and conservative.
- Blast radius is addressed at least qualitatively.
- Architecture-sensitive surfaces are named or marked unknown.
- The recommendation does not overclaim from weak evidence.
