---
description: L0-L3 cost and side-effect levels for source inspection, command discovery, verification, and debug loops.
metadata:
  tags: [cost-levels, side-effects, execution, verification, debug-loop]
---

# Cost / Side-Effect Levels

High-cost, high-side-effect, or high-uncertainty operations must be proposed and approved before execution.

## L0: Source Inspection

Default for Project Map, Module Map, and Task Recon.

Allowed:

- file names and directory shape
- static source snippets
- imports, symbols, class/function names
- concise README or architecture docs
- targeted source search

Not allowed:

- running project code
- tests, builds, linters, typecheckers, installs, benchmarks
- dependency/environment validation
- debug/repair loops
- file writes

## L1: Metadata / Command Discovery

Allowed:

- identify candidate commands from docs/config
- identify candidate tests by path/symbol
- inspect config only enough to understand source layout or command hints

Not allowed:

- executing commands
- validating command success
- installing dependencies
- treating command hints as verified runtime facts

## L2: Execution / Verification

Requires explicit approval and command scope.

Allowed:

- run approved commands only
- summarize output concisely
- report failures honestly

Not allowed:

- broadening command scope silently
- long log dumps
- follow-up debug commands outside approval
- edits or repair loops unless separately approved

## L3: Debug / Repair Loop

Requires separate explicit approval with:

- target error or behavior
- approved files
- approved commands
- maximum iterations
- stop conditions
- dependency/install/generated-file policy

Default limit: one iteration unless the user approves more.

## Escalation Rule

Never move from a lower level to a higher level without stating:

1. current level;
2. requested next level;
3. reason for escalation;
4. expected command/file scope;
5. cost or side-effect risk;
6. approval needed.
