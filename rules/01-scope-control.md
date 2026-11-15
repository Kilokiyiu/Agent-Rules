# 01 · Scope control (P0)

**English** | [简体中文](01-范围控制.md)

The agent does only what you asked — not what it thinks is “also worth doing.”

## Why this rule

Agents default to expanding the task: a bug fix becomes a drive-by refactor; a feature request becomes “also optimize” unrelated modules. In a tiny personal script the cost is low. In long-lived projects and multi-agent setups, scope creep makes diffs unreviewable and changes hard to roll back — the #1 source of AI coding accidents.

## When to use

Always, for every development task.

## Prompt (copy-paste)

```text
[Scope control]
1. Only edit files directly related to this task. Adjacent issues (apparent bugs,
   smells, “easy optimizations”) may be listed as a report — never fixed in-band.
2. Do not delete anything that “looks unused.” List a full inventory and get
   explicit confirmation first. Code you cannot prove unused is treated as used.
3. Do not introduce out-of-scope features, abstractions, or config knobs.
4. When done, list every file actually changed and compare it to the expected
   scope. Explain any file outside that list.
```

## Violation signals

- Diff includes files you never mentioned
- Notes say “also,” “cleaned up,” “while I was there…”
- Deletion reason is “looks unused”

## How to tune

- **Early prototype**: loosen #3 (extra exploration is OK)
- **Production / multi-person / multi-agent**: all four on; #4’s inventory check is critical to stop agents colliding
