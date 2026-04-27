---
description: Documentation routing, freshness control, and evidence citation format for durable agent context.
metadata:
  tags: [documentation, routing, freshness, evidence, handoff]
---

# Documentation Routing

## Recommended Layout

```text
AGENTS.md

docs/
  agent/
    README.md
    project-map.md
    modules/
      index.md
      auth.md
      api.md
      data-pipeline.md
    handoffs/
      2026-04-26-fix-login-bug.md
    decisions/
      0001-module-boundary.md
```

Do not create empty module docs just because directories exist. Create durable docs only after verified Project Map, Module Map, Distill Handoff, or accepted decisions.

## Destination Rules

| Finding type | Destination | Write when |
| --- | --- | --- |
| Global repo rule, command, or constraint | `AGENTS.md` | Stable, verified, and applies to future tasks. |
| Project overview or navigation | `docs/agent/project-map.md` | Verified during Project Map and useful across tasks. |
| Module boundary or stable module behavior | `docs/agent/modules/*.md` | Verified during Module Map or implementation. |
| Module index | `docs/agent/modules/index.md` | Module list or ownership map is verified. |
| Temporary task continuation state | `docs/agent/handoffs/*.md` | Needed for another agent or later session to continue. |
| Architecture, module-boundary, dependency, or public API decision | `docs/agent/decisions/*.md` | Decision is accepted or explicitly proposed with status. |
| One-off debug detail | Discard | Not reusable. |
| Unverified guess | Discard or handoff with warning | Never store as durable fact. |

## Freshness / Last Verified

Durable documentation patches must include freshness when they describe module behavior, commands, tests, public APIs, data flow, or project structure.

Use this block:

```markdown
## Freshness / Last Verified

- Date: YYYY-MM-DD
- Branch / commit: [branch and commit if available, otherwise "unknown"]
- Last verified by: [agent/person]
- Evidence:
  - Code: `path/to/file.ts::symbolName`
  - Candidate test or executed test evidence: `path/to/file.test.ts::testName`
  - Config: `package.json::scripts.test`
  - Command run, only if approved and actually run: `npm test -- path/to/file.test.ts`
- Notes: [short caveat or "none"]
```

Do not store stale plans as current truth. If freshness is unknown, mark it unknown rather than omitting it.

## Evidence Citation Format

Prefer file path plus symbol. Do not require line numbers as a hard rule.

Supported evidence forms:

- Code: `src/auth/session.ts::validateSession`
- Candidate test or executed test evidence: `src/auth/session.test.ts::rejectsExpiredToken`
- Config: `package.json::scripts.test`
- Command run, only if approved and actually run: `npm test -- session.test.ts`
- Output: `[short result summary]`
- Document: `docs/api.md::Authentication section`

Behavior claims should be written as:

```markdown
Confirmed:
- Token expiry is checked in `src/auth/session.ts::validateSession`.

Evidence:
- Code: `src/auth/session.ts::validateSession`
- Candidate test or executed test evidence: `src/auth/session.test.ts::rejectsExpiredToken`
```

## Do Not Store

- Unverified guesses as durable facts.
- One-off debugging noise.
- Temporary local paths unless needed for continuation.
- Agent process narration.
- Old plans without status.
- User preferences unless the user explicitly asks to preserve them.
