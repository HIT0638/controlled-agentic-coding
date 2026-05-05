---
name: tb-coding-workflow:verify-review
description: Verify completed changes, inspect diffs, and report untested risks honestly.
argument-hint: "[task, changed files, approved verification commands if any]"
---

Use the Controlled Agentic Coding Workflow Skill.

Run prompt template:
`prompts/verify_review.md`

User request:
$ARGUMENTS

Important:
- This command is only an entrypoint.
- It does not grant edit approval.
- Run only verification commands that are explicitly approved or clearly requested within this command's scope.
- Do not modify files.
- Do not enter an L3 debug/repair loop without separate approval.
- Distinguish executed verification, inspection-based verification, and unverified assumptions.
- Do not claim success for checks not run.
