---
description: Detailed approval semantics and mode transition rules for the controlled agentic coding workflow.
metadata:
  tags: [approval, transitions, state-machine, scope-control]
---

# Approval and Transitions

## Approval Semantics

Vague task requests are not edit approval. Edit approval must clearly authorize file modification.

Counts as edit approval:

- "Apply this plan."
- "Proceed with the approved plan."
- "You may edit these files."
- "Modify `path/to/file`."
- "Make this change in `path/to/file`."
- "Use Guarded Act for the approved files."

Does not count as edit approval:

- "Fix this."
- "Look into this."
- "What is wrong?"
- "Can you improve this?"
- "Continue."
- "What would you change?"
- "Review this."
- "Plan this."

If approval is ambiguous, stay read-only and ask for clarification or produce a Plan Change.

## Transition Rules

| From | To | Allowed when | Must stop when |
| --- | --- | --- | --- |
| Project Map | Module Map | The target module or subsystem is known. | Repository purpose, commands, or main entry points are still unknown. |
| Project Map | Task Recon | The task target is already clear enough to inspect narrowly. | The task is broad, repo-wide, or underspecified. |
| Module Map | Task Recon | Module boundary, entry points, and direct dependencies are sufficiently understood. | The module boundary or ownership is unclear. |
| Task Recon | Plan Change | Relevant files, current static behavior, likely change points, candidate tests, and risks are known. | Change location, candidate test path, or risk profile is unclear. |
| Plan Change | Guarded Act | The user approved the plan or explicitly approved a narrow edit scope. | Approval is missing or ambiguous. |
| Guarded Act | Verify Review | Implementation stayed within approved files and scope. | An unapproved file, dependency, schema change, public API change, or broad refactor is needed. |
| Verify Review | Guarded Act | The user approves a follow-up fix within a clear scope. | The failure changes scope or invalidates the plan. |
| Any | Distill Handoff | Reusable context, unfinished task state, or durable decisions should be preserved. | Proposed docs would contain guesses, stale plans, or task noise. |

Do not enter a later mode just because it is convenient. If entry criteria are not met, use the earlier mode or stop.

## Direct Narrow Approval

If the user directly approves a narrow edit without a separate plan, Guarded Act may start only when:

- approved files are explicit, or the edit target is unambiguous;
- the change is small enough to fit the approved scope;
- no dependency, schema, public API, migration, runtime validation, command execution, or broad refactor is required.

If any condition fails, return to Task Recon or Plan Change.
