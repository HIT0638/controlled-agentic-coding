---
description: Prompt template for read-only task reconnaissance before planning a feature, bug fix, or refactor.
metadata:
  tags: [mode, task-recon, context-pack, read-only]
---

Use the Controlled Agentic Coding Workflow Skill.

Mode: task-recon

Default level: L0 Source Inspection. May produce L1 candidate verification commands. Must not enter L2 or L3 without explicit approval.

Task:
[TASK DESCRIPTION]

Goal:
Find the smallest sufficient context needed to plan this task.

Entry criteria:
- A concrete feature, bug fix, refactor, or investigation target exists.
- The current context is insufficient for a safe implementation plan.
- Edit approval is absent or planning has not yet happened.

Rules:
- Read-only.
- Do not modify files.
- Do not propose code yet.
- Do not expand beyond the task.
- Stop when you can identify relevant files, risks, and candidate tests.
- Identify candidate related tests; do not run them unless the user explicitly approves verification commands.

Progressive disclosure:
- Start from file names, search hits, imports, symbols, and small slices.
- Read only files directly relevant to the task or direct dependencies.
- Prefer targeted searches and excerpts over full-file reads.
- Read deeper only when needed to identify static behavior, risks, candidate tests, or likely change points.
- If more context is needed, name the exact next area and why it matters.

Must not:
- Write implementation steps.
- Draft patches.
- Promise a specific fix.
- Treat likely change locations as approved files.
- Read unrelated modules just to be thorough.
- Read entire modules or test suites when a targeted slice is enough.
- Run tests, builds, linters, installs, benchmarks, examples, or project entrypoints without explicit verification approval.

Output:
## Context Pack

### Relevant files
| File | Why relevant | Confidence |

### Entry points
...

### Current behavior
...

### Likely change points
...

### Candidate related tests
List candidate tests by path/symbol for later verification. Do not run them or report execution results unless explicitly approved and actually run.

### Risks
...

### Unknowns
...

### Recommendation
Choose one:
A. ready to plan
B. inspect one more area
C. ask user for missing input
D. stop because task is unsafe or too broad

Exit criteria:
- Relevant files and entry points are identified with confidence.
- Current behavior is grounded in static file evidence or explicitly approved command output.
- Likely change points are separated from approved edit scope.
- Risks, unknowns, and candidate tests are explicit.

If blocked:
- Ask for the smallest missing input or name exactly one more area to inspect.
- Do not fill gaps with assumptions.
