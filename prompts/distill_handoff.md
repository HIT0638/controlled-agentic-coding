---
description: Prompt template for ending a task, preserving durable context, and separating stable documentation from temporary handoff notes.
metadata:
  tags: [mode, handoff, documentation, context-distillation]
---

Use the Controlled Agentic Coding Workflow Skill.

Mode: distill-handoff

Default level: documentation proposal only. Does not imply file writes, L2 execution, or L3 debug/repair.

Task:
[TASK]

Current state:
[SUMMARY]

Entry criteria:
- A task is ending, pausing, or transferring context.
- Reusable context may exist.
- The user has approved documentation edits, or this pass will only propose them.

Rules:
- Separate long-term knowledge from task-specific notes.
- Do not update AGENTS.md unless the knowledge is stable and global.
- Do not update module docs unless claims are verified.
- Mark unverified information clearly.
- Discard temporary findings that do not help a future agent.

Must not:
- Store unverified guesses as durable facts.
- Put one-off debugging noise into AGENTS.md.
- Preserve stale plans as current truth.
- Write docs without approval.
- Turn handoffs into project documentation.

Output:
## Handoff Summary

## Documentation Decision

### Update AGENTS.md?
Yes/No. Why?

### Update module docs?
Yes/No. Which module? Why?

### Create task handoff?
Yes/No. Why?

## Proposed Documentation Patch
Show proposed changes only.

Durable documentation patches must include `Freshness / Last Verified` when they describe module behavior, public APIs, data flow, project structure, or commands/tests that were explicitly approved and actually run.

Use this evidence format when possible:
- Code: `path/to/file.ts::symbolName`
- Candidate test: `path/to/file.test.ts::testName`
- Config evidence: `package.json::scripts.test`
- Command run, only if explicitly approved and actually run: `npm test -- path/to/file.test.ts`
- Output, only if observed from an approved run: `[short result summary]`

Exit criteria:
- Documentation destination is justified.
- Long-term facts are separated from temporary task state.
- Unverified information is marked or discarded.
- Proposed patch is shown without applying it unless approved.

If blocked:
- Produce a handoff-only summary.
- Ask for documentation approval if durable updates are needed.

Stop before editing docs.
