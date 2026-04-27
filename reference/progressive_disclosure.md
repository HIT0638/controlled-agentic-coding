---
description: Progressive disclosure rules for low-cost project exploration, task reconnaissance, and file reading.
metadata:
  tags: [progressive-disclosure, project-map, task-recon, file-reading, token-control]
---

# Progressive Disclosure

Project Map, Module Map, and Task Recon should gather enough static source context without treating "understand the project" as permission to read large parts of the repository or execute project code.

Default strategy:

```text
file list first -> names and structure -> manifests and indexes -> targeted excerpts -> justified expansion
```

The goal is sufficiency, not an arbitrary token budget. Read more when needed, but make each expansion intentional.

## Project Map Reading Strategy

First pass:

- Inspect file lists and top-level directory shape before file contents.
- Use file names, directory names, source manifests, configs, and entrypoint names as primary evidence.
- Read content only when names, structure, or config are insufficient to answer Project Map questions.
- When content is needed, read the smallest useful excerpt first.
- Check size or line count before opening suspected large files.
- Prefer `rg --files`, targeted `rg`, `find` depth limits, `ls`, `wc -l`, and small `sed -n` slices.

Avoid during Project Map unless explicitly justified:

- lockfiles
- dependency files read for dependency analysis
- generated files
- vendored code
- build outputs
- coverage
- logs
- large fixtures
- large data files
- notebook outputs
- entire test suites
- full implementation files when names and signatures are enough

If the first pass is insufficient, expand by naming:

- what was already learned;
- what remains unknown;
- which files or areas should be inspected next;
- why those reads are needed.

Do not stop just because a default starting point was reached. Stop when the next read would be broad, low-signal, or unjustified.

## Task Recon Reading Strategy

Task Recon may read deeper than Project Map, but only along the task path.

- Start from the specific symptom, feature, error, symbol, or module named by the user.
- Use targeted search hits before opening files.
- Read direct dependencies only when needed to understand the task.
- Read enough to identify relevant files, current behavior, likely change points, tests, risks, and unknowns.
- Do not read unrelated modules "just in case."

## Red Flags

Stop when:

- You are reading many files to be thorough.
- You are opening broad implementation files before using file names, imports, or search hits.
- You are reading lockfiles, dependency details, generated files, large data, logs, or notebook outputs during Project Map.
- You cannot explain why the next file is needed for the current mode output.
- The next read is broad or low-signal rather than tied to a specific unknown.
