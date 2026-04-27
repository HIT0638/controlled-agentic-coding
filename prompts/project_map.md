---
description: Prompt template for creating a compact source-only repository map before deeper coding work.
metadata:
  tags: [mode, project-map, repository-onboarding, read-only]
---

Use the Controlled Agentic Coding Workflow Skill.

Mode: project-map

Default level: L0 Source Inspection. L1 command hints only if cheaply visible and directly useful. Must not enter L2 or L3.

Goal:
Create a compact source-code map for future AI coding agents.

Entry criteria:
- Source-level repository understanding is needed.
- The current conversation lacks a reliable project map.
- The task is broad enough that module-only inspection would be premature.

Rules:
- Read-only.
- Do not modify files.
- Do not read the whole repository.
- Start from file names, directory shape, source manifests, and high-signal source entry files.
- Prefer navigation and boundaries over implementation details.
- Mark claims as confirmed / inferred / unknown.
- Treat runtime, dependency, install, test, build, lint, benchmark, and environment validation as out of scope unless explicitly requested and escalated out of Project Map.

Progressive disclosure:
- First inspect file lists and directory shape before reading file contents.
- Use file names, directory names, source manifests, and entrypoint names as primary evidence.
- Read content only when names, structure, or config are insufficient to answer Project Map questions.
- When content is needed, read the smallest useful excerpt first.
- Check size or line count before opening suspected large files.
- If the first pass is insufficient, expand by naming what remains unknown, which area to inspect next, and why.

Inspect first:
- file list / top-level tree
- README or source overview, if concise
- source package/module manifest, only enough to identify layout and entry points
- docs index, only if it explains source architecture
- main source entry points

Must not:
- Edit or create `AGENTS.md`.
- Read the whole repository.
- Read lockfiles, dependency lists for their own sake, generated files, vendored code, build outputs, coverage, logs, large fixtures, large data files, or notebook outputs during Project Map.
- Read broad file contents when names and structure are enough.
- Run tests, builds, linters, typecheckers, package installs, benchmarks, examples, scripts, notebooks, servers, or project entrypoints.
- Validate dependencies, runtime environment, installability, or command correctness.
- Produce module implementation details beyond navigation-level summary.

Output:
1. Source-level project purpose
2. Apparent language/framework only if obvious from source files
3. Major source module map
4. Main source entry points
5. Suggested next reading order
6. Unknowns
7. Documentation recommendation, not a full draft
8. Recommended next action

Exit criteria:
- A future agent can identify the source purpose, major modules, entry points, and what to read next.
- Runtime, dependency, install, test, build, lint, and environment status are not claimed.
- Unknowns are explicit.

If blocked:
- State what root files were missing.
- Mark unsupported claims as unknown.
- Recommend Module Map, Task Recon, or clarification.

Stop before writing files.
