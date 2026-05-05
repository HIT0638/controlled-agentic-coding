---
name: tb-coding-workflow:distill-handoff
description: Preserve durable context and separate stable documentation from temporary handoff notes.
argument-hint: "[task summary and current state]"
---

Use the Controlled Agentic Coding Workflow Skill.

Run prompt template:
`prompts/distill_handoff.md`

User request:
$ARGUMENTS

Important:
- This command is only an entrypoint.
- It does not grant edit approval.
- It does not grant command approval.
- Default is documentation proposal only.
- Do not write docs unless the user explicitly approves documentation edits.
- Do not store unverified guesses as durable facts.
- Separate long-term knowledge from task-specific notes.
