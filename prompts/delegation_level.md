---
description: Prompt template for assigning an AI delegation level based on codebase position, risk, and verifiability.
metadata:
  tags: [delegation, risk, planning, verification]
---

Use the Controlled Agentic Coding Workflow Skill and the AI Delegation Risk Add-on.

Workflow mode: inherit current mode
Add-on: delegation-level
Default level: inherit the current workflow mode. Do not escalate side effects.

Inputs:
- task: [TASK]
- leaf_or_core: [OPTIONAL OUTPUT OR SUMMARY]
- risk_map: [OPTIONAL OUTPUT OR SUMMARY]
- verifiable_abstraction: [OPTIONAL OUTPUT OR SUMMARY]

Goal:
Decide how much implementation ownership AI may safely take.

Rules:
- Delegation judgment does not equal edit approval.
- Delegation judgment does not equal command approval.
- If prior add-on outputs exist, use them.
- If they do not exist, make a compact inline assessment and mark the result `provisional`.
- Stay conservative when codebase position, blast radius, or verification shape is unclear.

Delegation levels:

- `D0`: Human-owned; do not delegate implementation.
- `D1`: AI exploration only.
- `D2`: AI draft under strict human plan and review.
- `D3`: AI scoped implementation with tests/review.
- `D4`: AI freer generation for disposable or low-risk leaf work.

Output:
## Delegation level
Choose one: `D0`, `D1`, `D2`, `D3`, `D4`

## Why
Tie the judgment to codebase position, risk, and verification shape.

## Human-owned parts
Name the architecture, contract, or review surfaces that must stay with a human.

## AI-owned parts
Name the implementation or exploration scope AI may own, if any.

## Required verification
List the minimum evidence needed before trusting the result.

## Stop conditions
Name what new finding should force a lower delegation level or human takeover.

## Raise / lower evidence
State what evidence would raise or lower the delegation level.

## Plan Change readiness
Choose one:
- ready for Plan Change
- needs more Task Recon
- needs human design review first

## Confidence
State whether the judgment is confirmed enough for planning or still `provisional`.

Exit criteria:
- The level is conservative and evidence-backed.
- Ownership boundaries are explicit.
- Verification obligations and downgrade triggers are explicit.
