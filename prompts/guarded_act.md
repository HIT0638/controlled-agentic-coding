---
description: Prompt template for implementing an explicitly approved plan with minimal scoped edits.
metadata:
  tags: [mode, guarded-act, implementation, minimal-diff]
---

Use the Controlled Agentic Coding Workflow Skill.

Mode: guarded-act

Default level: approved file editing only. Guarded Act does not imply L2 execution or L3 debug/repair.

Approved plan:
[PASTE PLAN]

Approved files:
[LIST FILES]

Entry criteria:
- User explicitly approved the plan or a narrow edit scope.
- Approved files are listed.
- The intended change can fit inside that scope.

Before editing:
- Check current diff/status when available.
- Identify existing user changes inside and outside approved files.
- Do not overwrite or revert unrelated user changes.
- If approved files already contain user changes, report that before editing.
- If user changes make the approved plan unsafe, stop and return to Plan Change.

Rules:
- Modify only approved files.
- Make the smallest working change.
- Do not refactor unrelated code.
- Do not change formatting unless required.
- Do not add dependencies.
- Stop if the implementation requires changing scope.
- After changes, summarize diff by file.

Must not:
- Edit unapproved files.
- Run tests, builds, linters, typecheckers, installs, examples, notebooks, servers, benchmarks, or project entrypoints unless separately approved as L2 for this mode.
- Run formatters that rewrite unapproved files.
- Add dependencies, migrations, snapshots, generated outputs, or lockfile changes unless approved.
- Continue after discovering the plan is wrong.
- Commit changes.

Scope expansion protocol:
If implementation needs an unapproved file or broader behavior change:
1. Stop editing.
2. State the file or behavior change needed.
3. State why the approved scope is insufficient.
4. State whether current edits are complete, incomplete, or should be revisited.
5. Return to Plan Change or ask for expanded approval.

Output:
1. Files changed
2. What changed
3. Why each change was necessary
4. Deviations from plan, if any
5. Candidate verification commands for a later Verify Review; do not run them here unless separately approved

Exit criteria:
- All edits stay within approved scope.
- Diff is minimal and explainable.
- Any deviations are reported.
- Next verification step is clear and not executed in Guarded Act unless separately approved.

Do not commit.
