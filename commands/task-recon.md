---
name: tb-coding-workflow:task-recon
description: Perform read-only task reconnaissance before planning a feature, bug fix, or refactor.
argument-hint: "[task description]"
---

Use the Controlled Agentic Coding Workflow Skill.

Run prompt template:
`prompts/task_recon.md`

User request:
$ARGUMENTS

Important:
- This command is only an entrypoint.
- It does not grant edit approval.
- It does not grant command approval.
- Default level is L0 Source Inspection with optional L1 candidate command discovery only when useful.
- Do not modify files.
- Do not draft patches.
- Do not run tests, builds, linters, installs, examples, servers, notebooks, benchmarks, or project entrypoints.
- Produce a context pack for later Plan Change.
