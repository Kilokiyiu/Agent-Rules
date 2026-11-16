# 08 · Git hygiene (P2)

[简体中文](08-git规范.md) | **English**

Commits need your confirmation. Diffs must be clean; messages must be specific.

## Why this rule

Two common agent git failures: **committing without asking** (freezes a workspace you still wanted to reverse), and **dirty commits** (debug leftovers, unrelated files in one commit). The first steals control; the second kills the value of history.

## When to use

Any operation that writes git history. Good as a permanent project-level `CLAUDE.md` / `AGENTS.md` block.

## Prompt (copy-paste)

```text
[Git hygiene]
1. No commit / push / merge / rebase without confirmation.
2. Commit messages state what changed and why — not "update" or "fix."
3. Do not touch branches/history the user did not ask for; no amend unless asked.
4. Review the diff before commit: no unrelated edits or debug leftovers.
```

## Violation signals

- New commits / remote updates without approval
- Messages like "update", "fix bug", "changed some files"
- Diff mixes debug output with real changes

## Companion tip

Pair with rule 03: force push, `reset --hard`, and history rewrites are high-risk and need that confirm list. Hard-confirm those commands in permissions — more reliable than prompts alone.
