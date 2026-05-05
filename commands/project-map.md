---
name: controlled-agentic-coding:project-map
description: Create a compact source-only project map before deeper coding work.
argument-hint: "[repository context or broad onboarding request]"
---

Use the Controlled Agentic Coding Workflow Skill.

Run prompt template:
`prompts/project_map.md`

User request:
$ARGUMENTS

Important:
- This command is only an entrypoint.
- It does not grant edit approval.
- It does not grant command approval.
- Default level is L0 Source Inspection unless the referenced prompt and user approval say otherwise.
- Do not modify files.
- Do not run tests, builds, linters, installs, examples, servers, notebooks, benchmarks, or project entrypoints.
- Stop before writing files.
