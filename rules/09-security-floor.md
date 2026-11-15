# 09 · Security floor (P2)

**English** | [简体中文](09-安全底线.md)

No secrets in source, validate external input, parameterize SQL — no exceptions.

## Why this rule

Demo-oriented generation takes shortcuts: hard-coded secrets, string-built SQL, trusting all input. Fine for a toy; in real environments each is a ready vulnerability. This rule does not require deep security expertise — only three fixed habits. High leverage.

## When to use

Anything touching real data, real deploy, or credentials. Pure offline toys may skip.

## Prompt (copy-paste)

```text
[Security floor]
1. Secrets, tokens, and credentials go in env vars or out-of-repo config —
   never hard-coded in source.
2. External input (user / network / files) must be validated before use.
3. SQL must be parameterized — no string concatenation.
4. Error messages must not leak internal paths or stack traces to end users.
```

## Violation signals

- `"sk-..."`, `"password=..."`, hard-coded tokens in code
- New endpoints using params with no checks
- SQL like `"... WHERE id = " + userInput`
- User-facing errors with full stacks and server paths

## Companion tip

Ignore `.env` (and similar) in `.gitignore`, and have the agent self-check these four items before every commit — cheap enough for a pre-commit checklist.
