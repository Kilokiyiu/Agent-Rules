# 06 · Test verification (P1)

**English** | [简体中文](06-测试验证.md)

Every change needs verification with real run output. Failures must not be papered over.

## Why this rule

Unconstrained agents often: edit → say “should be fine” → stop. “Should” often means no test ran. Worse: delete or skip failing tests to look green — the project looks healthy while risk is buried.

## When to use

After every code change. For bugs, insist on reproduce → root cause → fix → verify. Skipping reproduce usually fixes the wrong thing.

## Prompt (copy-paste)

```text
[Test verification]
1. After every code change, run build/test commands and return real output.
2. If the project has no tests, at least compile / syntax-check / minimal run,
   and state what was and was not verified.
3. Bug fixes: reproduce → root cause → fix → verify the original scenario.
   Do not skip reproduce and jump to edits.
4. On failure, report the real output. Do not delete or skip tests to go green.
```

## Violation signals

- “Should work” / “theoretically fine” with no output
- Test count drops or failures vanish from the list
- Bug fix with no reproduction steps, only a guessed edit

## How to tune

- **No test infra**: downgrade #1 to “compile + minimal run”; never loosen #4
- **With CI**: upgrade “return real output” to “wait for CI and attach the run link”
