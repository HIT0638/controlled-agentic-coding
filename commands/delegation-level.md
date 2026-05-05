---
name: tb-coding-workflow:delegation-level
description: Decide how much implementation ownership AI may safely take based on position, risk, and verifiability.
argument-hint: "[task plus optional leaf-or-core/risk-map/verifiable-abstraction outputs]"
---

Use the Controlled Agentic Coding Workflow Skill and the AI Delegation Risk Add-on.

Run prompt template:
`prompts/delegation_level.md`

User request:
$ARGUMENTS

Important:
- This command is only an entrypoint.
- This is add-on analysis, not a new workflow mode.
- It does not grant edit approval.
- It does not grant command approval.
- It inherits the current workflow mode and side-effect level.
- D0-D4 are delegation / ownership judgments, not permission levels.
- Even D3 or D4 still requires explicit approval before file modification or command execution.
