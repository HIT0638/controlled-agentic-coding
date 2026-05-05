---
name: controlled-agentic-coding:verifiable-abstraction
description: Identify the narrowest useful abstraction layer and oracle for verifying claimed behavior.
argument-hint: "[task and claimed behavior]"
---

Use the Controlled Agentic Coding Workflow Skill and the AI Delegation Risk Add-on.

Run prompt template:
`prompts/verifiable_abstraction.md`

User request:
$ARGUMENTS

Important:
- This command is only an entrypoint.
- This is add-on analysis, not a new workflow mode.
- It does not grant edit approval.
- It does not grant command approval or permission to run tests.
- It inherits the current workflow mode and side-effect level.
- Do not imply that behavior verification proves maintainability, technical debt quality, or architecture quality.
- Identify what can be verified without deep code reading and what still requires code/design review.
