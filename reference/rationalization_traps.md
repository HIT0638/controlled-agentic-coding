---
description: Common agent rationalizations and required counters for the controlled agentic coding workflow.
metadata:
  tags: [anti-rationalization, red-flags, discipline, scope-control]
---

# Rationalization Traps

| Excuse | Required behavior |
| --- | --- |
| "This is small, I can edit directly." | Small edits still require approval unless approval was already explicit. |
| "I know where the bug is." | Knowledge does not replace recon when context is insufficient. |
| "The user said continue." | Continue is not edit approval unless approval was already explicit. |
| "The user probably wants cleanup too." | Do not expand scope silently. |
| "Formatting is harmless." | Formatting is a file modification and needs approval. |
| "The formatter only changed style." | Formatting churn outside approved scope is scope expansion. |
| "I can test later." | Verification status must be explicit before final handoff. |
| "The command probably passed." | Never report success for commands not run or not observed. |
| "Running tests confirms the map." | Exploration maps source structure only. Runtime validation is separate and requires explicit approval. |
| "Tests are read-only." | Tests execute project code and can produce large output; they are not source exploration. |
| "I should check dependencies." | Dependency and environment validation are out of scope unless explicitly requested. |
| "This extra dependency would help." | Dependencies require explicit justification and approval. |
| "The lockfile change is automatic." | Lockfile changes are edits and must be approved. |
| "Generated files are not source." | Generated outputs are file changes and still need approval. |
| "Docs should capture everything I found." | Durable docs should contain stable, verified, reusable knowledge only. |
| "This handoff can become module docs." | Handoffs are task state; module docs require verified durable claims. |

## Red Flags

Stop when:

- You are about to edit before approval.
- You need to touch a file outside the approved scope.
- You found that the plan depends on an unverified assumption.
- You need a new dependency, schema change, migration, public API change, or broad refactor.
- Tests fail for reasons you do not understand.
- Existing user changes may be overwritten.
- Verification requires unavailable, unsafe, or unapproved commands.
