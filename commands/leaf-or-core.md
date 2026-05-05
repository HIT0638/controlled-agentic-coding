---
name: controlled-agentic-coding:leaf-or-core
description: Classify whether a task touches leaf code, architecture-sensitive core code, mixed boundaries, or unknown areas.
argument-hint: "[task, files, module, diff, or artifact]"
---

Use the Controlled Agentic Coding Workflow Skill and the AI Delegation Risk Add-on.

Run prompt template:
`prompts/leaf_or_core.md`

User request:
$ARGUMENTS

Important:
- This command is only an entrypoint.
- This is add-on analysis, not a new workflow mode.
- It does not grant edit approval.
- It does not grant command approval.
- It inherits the current workflow mode and side-effect level.
- Classify conservatively when evidence is weak.
- D0-D4, if referenced, are delegation / ownership judgments, not permission levels.
