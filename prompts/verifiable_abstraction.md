---
description: Prompt template for finding the best abstraction layer and oracle for verifying claimed behavior with minimal sufficient evidence.
metadata:
  tags: [delegation, verification, abstraction, oracle]
---

Use the Controlled Agentic Coding Workflow Skill and the AI Delegation Risk Add-on.

Workflow mode: inherit current mode
Add-on: verifiable-abstraction
Default level: inherit the current workflow mode. Do not escalate side effects.

Task:
[TASK]

Claimed behavior:
[BEHAVIOR]

Goal:
Find the narrowest useful abstraction where the behavior can be checked honestly.

Rules:
- Do not imply that behavior verification proves maintainability or design quality.
- Prefer the smallest verification level that meaningfully covers the claim.
- If the output is hard to inspect, recommend making it more human-readable, inspectable, or testable when that fits scope.
- Distinguish what can be checked without deep code reading from what still requires code or design review.
- Verification design does not grant command approval or permission to run tests.

Verification oracle examples:

- expected output
- invariant
- differential comparison
- golden file
- property check
- stress/failure injection result
- human-readable artifact
- log/metric signal

Output:
## What property must hold?

## Verification level
Choose the best fit:
- function
- module contract
- data result
- integration behavior
- system behavior
- product behavior
- operational signal

## Minimal evidence needed

## Verification oracle
Name the best oracle or small set of oracles for this case.

## What can be verified without deep code reading

## What still requires code/design review

## Technical debt caveat
State what this verification would still fail to measure.

## Suggested acceptance checks
List the smallest meaningful checks, spot checks, human-readable outputs, or stress checks.
Each suggested acceptance check should name the property and oracle it covers.

## Confidence
State whether the proposed verification layer is strong, partial, or weak, and why.

Exit criteria:
- The verification layer matches the real claim.
- The oracle is concrete enough to guide later checks.
- Unmeasured design or debt risks remain explicit.
