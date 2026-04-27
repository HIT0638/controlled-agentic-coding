---
description: Prompt template for turning a task context pack into a concrete implementation plan before edits.
metadata:
  tags: [mode, plan-change, implementation-plan, approval-gate]
---

Use the Controlled Agentic Coding Workflow Skill.

Mode: plan-change

Default level: L0/L1 planning only. May list candidate L2 verification commands, but must not run them.

Task:
[TASK]

Context pack:
[PASTE OR REFERENCE CONTEXT PACK]

Goal:
Create a minimal implementation plan.

Entry criteria:
- Task Recon produced enough context, or the user provided equivalent context.
- Relevant files, risks, and candidate verification paths are known.
- No edits have been made for this task unless already approved.

Rules:
- Do not edit files.
- Do not write code yet.
- Respect existing module boundaries.
- No new dependency unless explicitly needed, justified, and approved later.
- No unrelated refactor.

Must not:
- Start implementation.
- Run tests, builds, linters, installs, examples, notebooks, servers, or project entrypoints.
- Hide risky changes inside broad wording.
- Omit files that are likely to be modified.
- Treat the plan itself as approval to edit.

Output:
## Objective

## Non-goals

## Proposed files to modify
These are not approved until the user explicitly confirms.

## Files not to modify

## Step-by-step plan

## Expected diff shape

## Candidate verification plan

## Risks

## Acceptance criteria

Exit criteria:
- The plan names proposed files and forbidden files.
- Each step has a narrow intent.
- Candidate verification commands are listed with confidence and are not run in this mode.
- Risks and stop conditions are explicit.

If blocked:
- Return to Task Recon for missing context.
- Ask for approval if the only blocker is edit permission.

Stop and wait for approval.
