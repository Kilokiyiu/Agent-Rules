# 07 · Style consistency (P1)

**English** | [简体中文](07-风格一致性.md)

New code must look like this repo’s code — not like generic “AI best practices.”

## Why this rule

Each session has a different style baseline: exceptions vs error codes; camelCase vs snake_case. Mixed together, the codebase shows visible seams — human vs which AI session. Cost is not only aesthetics: readers switch habits, maintainers edit the wrong place. The core move is **read before write**, not write then reformat.

## When to use

All work on an existing codebase. Not for greenfield repos (you set the style then).

## Prompt (copy-paste)

```text
[Style consistency]
1. Match existing naming, indentation, error handling, and layout. Read sibling /
   similar files before editing.
2. Before finishing, name which existing files you mirrored (traceability).
3. Do not introduce patterns foreign to the repo (e.g. error codes everywhere in
   an exceptions-based codebase) unless the user confirms a style change.
4. If conventions are unclear, ask — do not invent “industry best practice.”
```

## Violation signals

- Two error-handling styles in one file
- Naming clashes next to neighbors (`getUserData` beside `fetch_user`)
- New comment formats or folder layers never seen in the repo

## Companion tip

If allowed, lock conventions in editorconfig / lint / formatter so this prompt only covers what config cannot — naming semantics, error patterns, module layout.
