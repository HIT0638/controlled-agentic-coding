# Controlled Agentic Coding

Public version of the controlled coding workflow skill for AI coding assistants.

It is designed for real codebases where agents face limited context, stale docs, hallucination risk, task drift, dirty worktrees, and incomplete verification.

## What It Does

This skill gives an agent a disciplined workflow:

- read before acting
- stay read-only until explicit approval
- change only approved scope
- verify honestly
- avoid unrelated cleanup
- preserve durable context without writing task noise into docs

The goal is not to make the agent do more. The goal is to make it safer, narrower, and easier to audit.

## Core Workflow Modes

| Mode | Purpose |
| --- | --- |
| Project Map | Understand repository structure and entry points |
| Module Map | Understand one module boundary |
| Task Recon | Gather task-specific context before planning |
| Plan Change | Turn recon into a concrete implementation plan |
| Guarded Act | Implement an explicitly approved plan |
| Verify Review | Review diffs and verification coverage honestly |
| Distill Handoff | Preserve durable context and temporary continuation state cleanly |

## AI Delegation Risk Add-on

The public version also includes an add-on layer for judging how much implementation ownership AI should safely take.

It is not a new workflow mode. It does not grant edit approval or command approval.

Included add-on prompts:

- `leaf_or_core`
- `risk_map`
- `verifiable_abstraction`
- `delegation_level`

## Slash Command Entrypoints

If the host CLI supports slash commands, the repository includes thin wrappers under `commands/`.

Core workflow commands:

- `/controlled-agentic-coding:project-map`
- `/controlled-agentic-coding:module-map`
- `/controlled-agentic-coding:task-recon`
- `/controlled-agentic-coding:plan-change`
- `/controlled-agentic-coding:guarded-act`
- `/controlled-agentic-coding:verify-review`
- `/controlled-agentic-coding:distill-handoff`

Add-on commands:

- `/controlled-agentic-coding:leaf-or-core`
- `/controlled-agentic-coding:risk-map`
- `/controlled-agentic-coding:verifiable-abstraction`
- `/controlled-agentic-coding:delegation-level`

These command files are only entrypoints. They do not change approval semantics, side-effect levels, edit permissions, or command permissions.

## Installation

Project-local install:

```bash
mkdir -p .claude/skills
cp -r controlled-agentic-coding .claude/skills/
```

Global install:

```bash
mkdir -p ~/.claude/skills
cp -r controlled-agentic-coding ~/.claude/skills/
```

## Example Usage

Prompt-style:

```text
Use controlled-agentic-coding.

Goal: fix a null-pointer crash when the parser receives empty input.
```

Slash command style:

```text
/controlled-agentic-coding:task-recon fix a null-pointer crash when the parser receives empty input
/controlled-agentic-coding:plan-change parser empty-input crash context pack
/controlled-agentic-coding:risk-map parser empty-input handling
```

## Repository Layout

```text
controlled-agentic-coding/
├── SKILL.md
├── commands/
├── prompts/
├── reference/
├── eval/
└── LICENSE
```

- [commands/](commands/) contains thin slash-command wrappers.
- [prompts/](prompts/) contains core workflow and add-on prompt templates.
- [reference/](reference/) contains approval, side-effect, documentation, and delegation rules.
- [eval/](eval/) contains scenarios for checking whether an agent follows the workflow correctly.

## License

MIT License. See [LICENSE](LICENSE).
