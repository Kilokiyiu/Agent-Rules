# 05 · Plan first (P1)

[简体中文](05-计划先行.md) | **English**

For medium/large work: plan first, get approval, then code. If the plan is wrong, stop and re-confirm.

## Why this rule

Default agent behavior is to start writing. Midway it may silently change direction. You get something that might look right while the process was out of your control. Planning moves the expensive “is the direction right?” question to the cheapest moment.

## When to use

Trigger on any of:

- Changes spanning 3+ files
- Multiple viable technical approaches (architecture, libraries, data shapes)
- Large effort or high irreversibility

## Prompt (copy-paste)

```text
[Plan first]
1. For tasks touching 3+ files, ~30+ minutes of work, or multiple viable
   directions: output a plan first (file list + what changes where + risks).
   Start only after confirmation.
2. After approval, stay in scope. If the plan is wrong mid-flight, stop, propose
   a new plan, and re-confirm.
3. If the user gave a goal but no approach, ask the key decisions (stack /
   structure). Do not silently invent architecture.
```

## Violation signals

- Long silent execution, then a finished dump with no decision checkpoints
- Mid-course redesign with no heads-up (surprise abstraction layers)
- “Build XX” → agent picks a framework and scaffolds alone

## How to tune

- **Early / exploratory**: may disable this rule for speed
- **Refactor / near ship**: must enable — wrong direction is most expensive here
- If you plan yourself first (e.g. ASCII sketch), change this to: “restate the plan, flag doubts, then execute after confirm”
