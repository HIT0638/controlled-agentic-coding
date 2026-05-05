---
name: tb-coding-workflow:plan-change
description: Turn task context into a concrete implementation plan before edits.
argument-hint: "[task and context pack]"
---

Use the Controlled Agentic Coding Workflow Skill.

Run prompt template:
`prompts/plan_change.md`

User request:
$ARGUMENTS

Important:
- This command is only an entrypoint.
- It does not grant edit approval.
- It does not grant command approval.
- Do not edit files.
- Do not write code.
- Do not run tests, builds, linters, installs, examples, servers, notebooks, benchmarks, or project entrypoints.
- Proposed files are not approved until the user explicitly confirms.
- Stop and wait for approval.
