# 10 · Frontend constraints (P2)

[简体中文](10-前端约束.md) | **English**

Implement UI against the existing design system and component library. No freestyle redesigns or framework swaps.

## Why this rule

UI is where agents freestyle hardest: add a button → recolor the page; fix a CSS bug → pull a second UI kit. Visual “correctness” is underdetermined, so models paste pretty patterns from training data instead of your system. Sometimes that looks nicer; often it fights your expectations.

## When to use

All UI work. Not when greenfield design is agent-led (then: propose direction → you confirm → implement).

## Prompt (copy-paste)

```text
[Frontend constraints]
1. Follow existing mockups / style tokens. Do not freestyle colors, spacing, or layout.
2. Do not swap component libraries or style frameworks. New pages reuse existing patterns.
3. Prefer existing variables for colors/sizes/spacing — no piles of magic numbers.
4. Responsive / browser targets: ask if the user did not specify. Do not assume.
```

## Violation signals

- Diff full of unrelated style churn
- Same screen type implemented two ways (old kit + new agent kit)
- Hard-coded colors/px that duplicate design tokens

## Companion tip

Pair with rule 07. If you have a token file (CSS variables / theme), name its path in the prompt — “where to look” beats “don’t freestyle.”
