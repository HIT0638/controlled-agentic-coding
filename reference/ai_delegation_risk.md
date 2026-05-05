---
description: Cross-cutting guidance for deciding what AI may safely own, what humans must control, and how to verify behavior at the right abstraction layer.
metadata:
  tags: [delegation, risk, verification, architecture, workflow]
---

# AI Delegation Risk Add-on

## Purpose

Help decide where and how much coding work may be delegated to AI without weakening the existing approval gates, side-effect controls, or verification discipline.

This add-on does not replace:

- human architecture review
- edit approval
- command approval
- runtime verification
- maintainability review

## Non-goals

This add-on must not:

- create a new permission level
- authorize edits or commands
- claim technical debt can be judged without reading relevant code
- turn weak evidence into a strong delegation recommendation
- become a universal checklist used without task-specific tailoring

## Integration With Existing Workflow

Use it as a cross-cutting layer inside existing modes:

- Task Recon: produce preliminary, read-only judgments
- Plan Change: convert those judgments into implementation and verification constraints
- Verify Review: assess whether executed and inspection-based verification actually covered the important risks

These add-ons are optional and selective. They should not become mandatory output sections for every task.
Use them when the task has meaningful AI delegation, production, architecture, unknown-unknown, or verification-abstraction risk.

Current mode rules still control side effects. A delegation judgment never grants edit approval or command approval.

## Component Roles

### 1. Leaf or Core

Question:
What kind of codebase position does this task touch?

Allowed classifications:

- `leaf`
- `core`
- `mixed`
- `unknown`

Use `mixed` or `core` aggressively when the task appears local but touches architecture-sensitive surfaces such as:

- shared or public APIs
- schemas or wire/data contracts
- auth or permission logic
- global config or feature flags with broad reach
- reusable abstractions or framework helpers
- migration logic
- transaction or concurrency boundaries
- high-reuse utilities

### 2. Risk Map

Question:
What hidden assumptions, failure modes, and unknown unknowns matter most here?

Default to the top 5-10 highest-value risks. Select categories based on artifact type and codebase position instead of filling a generic checklist.

### 3. Verifiable Abstraction

Question:
At what abstraction layer can the claimed behavior be checked with minimal sufficient evidence?

Possible levels include:

- function
- module contract
- data result
- integration behavior
- system behavior
- product behavior
- operational signal

Behavior can sometimes be verified without reading every implementation detail. That does not prove:

- low technical debt
- good abstraction boundaries
- maintainability
- safe future change cost
- sound architecture

### 4. Delegation Level

Question:
Given position, risk, and verification shape, how much implementation ownership can AI take?

Delegation levels:

- `D0`: Human-owned; do not delegate implementation.
- `D1`: AI exploration only.
- `D2`: AI draft under strict human plan and review.
- `D3`: AI scoped implementation with tests/review.
- `D4`: AI freer generation for disposable or low-risk leaf work.

`D4` still does not allow touching unapproved files, shared interfaces, schemas, public contracts, or running commands without approval.

These are ownership levels, not side-effect levels.

## Evidence Discipline

Separate:

- confirmed
- inferred
- unknown

If evidence is weak, the delegation recommendation must stay conservative.

If outputs are hard to inspect, prefer changing the plan so results become more human-readable, inspectable, or testable, as long as that stays within approved scope.

## Verification Boundaries

Useful verification oracles may include:

- expected output
- invariant
- differential comparison
- golden file
- property check
- stress or failure-injection result
- human-readable artifact
- log or metric signal

Choose the smallest oracle that meaningfully covers the risk.

If no trustworthy oracle exists, that is itself a reason to reduce delegation confidence.

## Technical Debt Boundary

Behavioral verification is necessary but incomplete.

Passing checks do not by themselves show that:

- the architecture is sound
- shared abstractions remain coherent
- technical debt is acceptable
- future modification cost is reasonable

For architecture-sensitive, reused, or contract-heavy code, human design review remains required even when behavior looks correct.
