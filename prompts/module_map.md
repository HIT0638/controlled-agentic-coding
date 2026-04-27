---
description: Prompt template for mapping one source module boundary, entry points, source dependencies, candidate tests, and risks without executing project code.
metadata:
  tags: [mode, module-map, module-boundary, read-only]
---

Use the Controlled Agentic Coding Workflow Skill.

Mode: module-map

Default level: L0 Source Inspection. L1 candidate tests/config hints only if directly useful. Must not enter L2 or L3.

Target module:
[MODULE NAME]

Scope:
[PATHS]

Goal:
Create a source-only module boundary map.

Entry criteria:
- Target module and scope paths are known.
- Repository-level context is sufficient or not needed.
- The task needs module ownership, entry points, or source dependency boundaries.

Rules:
- Read-only.
- Source inspection only; do not execute project code.
- Do not inspect unrelated modules unless directly imported or called by source evidence.
- Do not modify docs yet.
- Every behavior claim must cite static file path and symbol/function name.
- Separate confirmed facts from assumptions.

Must not:
- Expand into unrelated modules without direct source dependency evidence.
- Run tests, builds, linters, typecheckers, installs, examples, notebooks, servers, or module entrypoints.
- Validate dependency installation, runtime environment, or command correctness.
- Follow call chains beyond what is needed to define the module boundary.
- Read entire test suites when candidate test names are enough.
- Propose implementation changes.
- Treat naming conventions as confirmed behavior.
- Update module docs before approval.

Answer:
1. Responsibility
2. Owns / does not own
3. Entry points
4. Key files
5. Important types/functions
6. Boundary-level data flow
7. Candidate related tests by filename/symbol only; do not run them
8. Known risks
9. Unknowns
10. Documentation recommendation or compact module doc draft if useful

Exit criteria:
- Responsibility and non-responsibility are explicit.
- Entry points and direct source dependencies are identified.
- Candidate tests and risks are listed or marked unknown without execution.
- Documentation recommendation contains only verified or clearly marked information.

If blocked:
- State which boundary, source dependency, or behavior could not be confirmed from static source evidence.
- Recommend one more focused inspection area or ask the user for scope.

Stop before editing.
