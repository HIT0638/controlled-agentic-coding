---
name: controlled-agentic-coding
description: >-
  Use when an AI coding agent is handling a non-trivial code task that needs scoped exploration, approval gates, minimal diffs, honest verification, or durable handoff notes.
metadata:
  category: discipline
  triggers: code change, bug fix, feature implementation, refactor, project exploration, project map, codebase onboarding, module map, task recon, approval gate, guarded act, verify review, handoff, 阅读项目, 探索项目, 项目地图, 代码库了解
---

# Controlled Agentic Coding Workflow

## Purpose

Keep AI coding agents controlled, auditable, and useful when working in real codebases with limited context, stale docs, hallucination risk, task drift, excessive refactoring, dirty worktrees, and incomplete verification.

## When to Use

Use this skill when any of these are true:

- A task may modify code, tests, configuration, docs, generated artifacts, schemas, dependencies, or lockfiles.
- The repository, module, or task boundary is not already clear in the current conversation.
- The user asks for a feature, bug fix, refactor, implementation plan, verification pass, review, or handoff.
- The agent must decide what to read, what may change, what must be verified, or what durable context should be preserved.

Do not use this skill for simple one-shot answers that do not inspect or change a workspace.

## Iron Rule

**Read first, bound the task, get approval before edits, change only the approved scope, verify honestly, and preserve only durable knowledge.**

Violating the letter of the workflow is violating the spirit of the workflow.

## Default State

Default behavior is read-only until the user explicitly approves edits.

Read-only allows searching, inspecting, summarizing, planning, and risk identification. It does not allow modifying, formatting, creating, deleting, installing, committing, or running destructive commands.

## Approval Semantics

Vague task requests are not edit approval. Edit approval must clearly authorize file modification.

Counts as edit approval:

- "Apply this plan."
- "Proceed with the approved plan."
- "You may edit these files."
- "Modify `path/to/file`."
- "Use Guarded Act for the approved files."

Does not count as edit approval:

- "Fix this."
- "Look into this."
- "What is wrong?"
- "Can you improve this?"
- "Continue."
- "Review this."
- "Plan this."

If approval is ambiguous, stay read-only and ask for clarification or produce a Plan Change.

Full rules: [reference/approval_and_transitions.md](reference/approval_and_transitions.md).

## Mode Selection

| Situation | Mode | Template |
| --- | --- | --- |
| First time understanding a repo | Project Map | [prompts/project_map.md](prompts/project_map.md) |
| Understanding one module boundary | Module Map | [prompts/module_map.md](prompts/module_map.md) |
| Before feature, bug fix, or refactor planning | Task Recon | [prompts/task_recon.md](prompts/task_recon.md) |
| Turning recon into an implementation plan | Plan Change | [prompts/plan_change.md](prompts/plan_change.md) |
| Implementing after explicit approval | Guarded Act | [prompts/guarded_act.md](prompts/guarded_act.md) |
| Checking completed changes | Verify Review | [prompts/verify_review.md](prompts/verify_review.md) |
| Ending a task or preparing context refresh | Distill Handoff | [prompts/distill_handoff.md](prompts/distill_handoff.md) |

When unsure, choose the earlier read-only mode. Do not skip directly to Guarded Act unless edit approval and allowed files are already explicit.

## Transition Rules

| From | To | Allowed when | Must stop when |
| --- | --- | --- | --- |
| Project/Module Map | Task Recon | Target and boundary are clear enough to inspect narrowly. | Repo, module, or ownership remains unclear. |
| Task Recon | Plan Change | Relevant files, behavior, likely change points, tests, and risks are known. | Change location, verification path, or risk profile is unclear. |
| Plan Change | Guarded Act | User approved the plan or a narrow edit scope. | Approval is missing or ambiguous. |
| Guarded Act | Verify Review | Implementation stayed within approved files and scope. | Unapproved files, dependencies, schemas, public APIs, or broad refactors are needed. |
| Verify Review | Guarded Act | User approves a follow-up fix within clear scope. | Failure changes scope or invalidates the plan. |
| Any | Distill Handoff | Reusable context or unfinished task state should be preserved. | Proposed docs would contain guesses, stale plans, or task noise. |

Full state machine: [reference/approval_and_transitions.md](reference/approval_and_transitions.md).


## Cost / Side-Effect Levels

L0: Source Inspection
Static file names, directory structure, source snippets, imports, symbols, and architecture notes. Default for Project Map, Module Map, and Task Recon.

L1: Metadata / Command Discovery
Identify candidate commands, tests, dependency clues, config, or CI hints from files. Do not execute or validate them.

L2: Execution / Verification
Run explicitly approved commands only. Requires command scope and purpose. Summarize output; do not paste long logs.

L3: Debug / Repair Loop
Iteratively run, diagnose, edit, and re-run. Requires separate explicit approval with file scope, command scope, maximum iterations, and stop conditions.

Never move from a lower level to a higher level without stating the reason and getting user approval.

## Non-Negotiable Rules

1. Read-only until approval.
2. Earlier mode when unsure.
3. Plan is not approval.
4. Modify only approved files.
5. Stop on scope expansion.
6. Verify honestly.
7. Preserve user changes.
8. Distill only durable knowledge.
9. Use progressive disclosure; prefer file names and structure before content, and justify broad reading.
10. Exploration modes are source-only by default: they do not inspect runtime behavior, validate dependencies, or run tests/builds/lint/installs/benchmarks/project code.
11. Never escalate from L0 to L1, L2, or L3 without explicit reason and approval when required.

See also [reference/progressive_disclosure.md](reference/progressive_disclosure.md) and [reference/command_file_safety.md](reference/command_file_safety.md).

## Red Flags - Stop

Stop and re-bound the task if any of these occur:

- You are about to edit before approval.
- You need to touch a file outside the approved scope.
- The plan depends on an unverified assumption.
- You need a dependency, schema change, migration, generated output, public API change, or broad refactor.
- Tests fail for reasons you do not understand.
- Verification requires commands that are unavailable, unsafe, or not approved.
- The user says "continue" but no edit approval exists.
- Existing user changes may be overwritten or mixed with agent changes.
- You are tempted to include unrelated cleanup.
- You are reading file contents broadly when filenames, manifests, or small slices would answer the current mode.
- You are opening many files to be thorough instead of answering the current mode's output questions.
- You are about to escalate from L0 source inspection to L1/L2/L3 without naming the reason and required approval.
- You are about to inspect dependency/runtime details or run tests, build, lint, install, benchmark, or execute project code during Project Map, Module Map, or Task Recon.

Common excuses and counters: [reference/rationalization_traps.md](reference/rationalization_traps.md).

## Documentation Routing Summary

| Finding type | Destination |
| --- | --- |
| Global repo rule, command, or constraint | `AGENTS.md` |
| Project overview or navigation | `docs/agent/project-map.md` |
| Module boundary or stable module behavior | `docs/agent/modules/*.md` |
| Temporary task continuation state | `docs/agent/handoffs/*.md` |
| Architecture, dependency, public API, or module-boundary decision | `docs/agent/decisions/*.md` |
| One-off debug detail or unverified guess | Discard, or handoff with warning if needed |

Durable docs describing behavior, commands, or tests must include freshness and evidence. Full rules and templates: [reference/documentation_routing.md](reference/documentation_routing.md).

## Enforcement Boundary

This skill is a behavioral protocol, not a deterministic sandbox.

For hard guarantees, combine it with:

- tool approval settings
- sandbox permissions
- hooks
- CI checks
- pre-commit checks
- branch protection
- human code review

Do not rely on this skill alone to prevent destructive operations.

## Evaluation

Use [eval/eval_scenarios.md](eval/eval_scenarios.md) to test whether agents follow the gates, scope rules, progressive disclosure, dirty-worktree protection, documentation routing, and verification discipline.
