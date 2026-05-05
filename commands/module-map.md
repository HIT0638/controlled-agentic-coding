---
name: controlled-agentic-coding:module-map
description: Map one module boundary, entry points, dependencies, candidate tests, and risks.
argument-hint: "[module name and paths]"
---

Use the Controlled Agentic Coding Workflow Skill.

Run prompt template:
`prompts/module_map.md`

User request:
$ARGUMENTS

Important:
- This command is only an entrypoint.
- It does not grant edit approval.
- It does not grant command approval.
- Default level is L0 Source Inspection unless the referenced prompt and user approval say otherwise.
- Keep the analysis source-only.
- Do not modify files.
- Do not run tests, builds, linters, installs, examples, servers, notebooks, benchmarks, or module entrypoints.
