---
name: controlled-agentic-coding:guarded-act
description: Implement an explicitly approved plan with minimal scoped edits.
argument-hint: "[approved plan and approved files]"
---

Use the Controlled Agentic Coding Workflow Skill.

Run prompt template:
`prompts/guarded_act.md`

User request:
$ARGUMENTS

Important:
- This command requires explicit edit approval and an approved file scope.
- It does not grant command approval.
- Modify only approved files.
- Make the smallest working change.
- Do not refactor unrelated code.
- Do not add dependencies, migrations, generated outputs, snapshots, or lockfile changes unless explicitly approved.
- Do not run tests, builds, linters, installs, examples, servers, notebooks, benchmarks, or project entrypoints unless separately approved as L2.
- Stop on scope expansion.
- Do not commit.
