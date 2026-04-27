---
description: Prompt template for verifying completed changes, inspecting diffs, and reporting untested risks honestly.
metadata:
  tags: [mode, verify-review, testing, diff-review]
---

Use the Controlled Agentic Coding Workflow Skill.

Mode: verify-review

Default level: L2 Execution / Verification. Must not enter L3 Debug / Repair Loop without separate explicit approval.

Task:
[TASK]

Changed files:
[FILES]

Entry criteria:
- There are completed changes to inspect, or the user asks to verify existing changes.
- The verification scope is known.
- Any commands to run are explicitly listed and approved, or the user clearly asks to run verification commands.

Rules:
- Run only approved relevant tests/checks.
- Prefer the narrowest command that covers the risk.
- Do not run follow-up commands after a failure unless they are within the approved command scope.
- Summarize command output; do not paste long logs.
- Do not claim success for commands not run.
- If a command fails, report failure clearly.
- List unverified edge cases.
- Review the diff for scope creep.

Must not:
- Modify files while verifying unless the user approves a follow-up Guarded Act.
- Hide failing checks behind a positive summary.
- Run broad test suites, builds, installs, or linters when a narrower approved check would answer the question.
- Diagnose, edit, or re-run in a loop after failure without L3 approval.
- Treat visual inspection as test execution.
- Approve changes that exceed the approved scope.

Output:
## Verification

### Commands Run
List only commands that were explicitly approved and actually run.

### Results

### Tested Scenarios

### Untested Scenarios

## Diff Review

Check:
- Approved files only.
- No unrelated formatting churn.
- No pre-existing user changes mixed with agent changes without being called out.
- No unexpected public behavior changes.
- No new dependencies, lockfile changes, snapshots, generated files, or migrations unless approved.
- No debug logs, dead code, or accidental TODOs.
- Tests cover the main risk when feasible.

## Residual Risks

## Recommendation
- approve
- request changes
- reject

Exit criteria:
- Commands and results are reported accurately and concisely.
- Untested areas are explicit.
- Diff scope is reviewed.
- Recommendation is tied to evidence.

If blocked:
- State which check could not run and why.
- Do not infer success.
- Recommend the smallest next verification step.
