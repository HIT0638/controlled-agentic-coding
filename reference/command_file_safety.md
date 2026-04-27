---
description: File, command, dirty worktree, dependency, formatter, generated-file, and verification safety rules.
metadata:
  tags: [safety, commands, dirty-worktree, dependencies, verification]
---

# Command and File Safety

Use [cost_side_effect_levels.md](cost_side_effect_levels.md) for L0-L3 escalation rules.

Treat commands by their effects, not their names.

## File Modification Rules

- A command that rewrites files is an edit and requires approval.
- A formatter is an edit unless run in check-only mode.
- A dependency install that changes lockfiles or manifests is an edit and requires approval.
- Snapshot updates, generated files, migrations, and codegen outputs are edits.
- Network access, escalation, destructive commands, and commits require explicit approval.


## Command Execution Boundaries

Project Map, Module Map, and Task Recon are source-inspection modes. They may run inspection commands only.

Allowed inspection examples:

- `rg --files`
- targeted `rg` searches
- `ls` / shallow `find`
- `wc -l` / file size checks
- small `sed -n` excerpts
- config inspection commands that do not execute project code

Not allowed during Project Map, Module Map, or unapproved Task Recon:

- tests: `pytest`, `npm test`, `cargo test`, `go test`, `mvn test`, `gradle test`
- builds: `npm run build`, `make`, `cargo build`, `mvn package`
- linters/typecheckers that scan the project: `npm run lint`, `tsc`, `ruff check`, `mypy`
- installs or dependency resolution: `npm install`, `pip install`, `poetry install`, `cargo fetch`
- examples, benchmarks, project entrypoints, migrations, servers, notebooks, or scripts that execute project logic

Exploration modes should not validate runtime behavior, dependencies, installability, or command correctness. If commands are visible, record them only as optional hints from docs/config when directly useful. Running them belongs only in Verify Review or a separately approved verification step with explicit command scope.

## Dirty Worktree Rules

Before editing, check current diff/status when available.

- Identify existing user changes inside and outside approved files.
- Do not overwrite, revert, or format unrelated user changes.
- If approved files already contain user changes, report that before editing.
- If user changes make the approved plan unsafe, stop and return to Plan Change.
- During Verify Review, check whether agent edits are mixed with pre-existing user changes.

If the environment has no version control or status command, state that dirty-worktree preflight is unavailable.

## Scope Expansion

If implementation needs an unapproved file or broader behavior change:

1. Stop editing.
2. State the file or behavior change needed.
3. State why the approved scope is insufficient.
4. State whether current edits are complete, incomplete, or should be revisited.
5. Return to Plan Change or ask for expanded approval.

## Verification Honesty

- If a command fails, report the failure.
- If a command was not run, do not claim it passed.
- If a check is unavailable, explain why and recommend the smallest next check.
- Do not treat visual inspection as test execution.
