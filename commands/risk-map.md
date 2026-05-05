---
name: controlled-agentic-coding:risk-map
description: Surface hidden assumptions, failure modes, and unknown unknowns for a scoped coding task.
argument-hint: "[task, file, module, API, pipeline, config, or diff]"
---

Use the Controlled Agentic Coding Workflow Skill and the AI Delegation Risk Add-on.

Run prompt template:
`prompts/risk_map.md`

User request:
$ARGUMENTS

Important:
- This command is only an entrypoint.
- This is add-on analysis, not a new workflow mode.
- It does not grant edit approval.
- It does not grant command approval.
- It inherits the current workflow mode and side-effect level.
- Focus on the top 5-10 highest-value risks.
- Every listed risk must include a concrete minimal check or explain why no reliable check is currently known.
