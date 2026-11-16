# 04 · Dependency management (P1)

[简体中文](04-依赖管理.md) | **English**

Before installing any new package, the agent must explain why and get your OK.

## Why this rule

Agents often reach for a library first — training data is full of “three lines with XX.” Long-term cost: a fatter tree, larger attack surface, painful upgrades, slower builds. Many needs are a dozen lines of stdlib. Once installed, removal costs more than writing those lines.

## When to use

- Installing any third-party library, framework, or CLI
- Upgrading or replacing dependency versions
- Stack choices (frontend framework, bundler, etc.)

## Prompt (copy-paste)

```text
[Dependency management]
1. Before any new dependency: state the problem, why existing deps/stdlib are
   not enough, and the maintenance cost. Install only after confirmation.
2. Priority: stdlib > reuse existing deps > small new dep > heavy framework.
3. Pin versions (lockfile / exact version). No loose ranges.
4. Do not pull a large framework to solve a small problem.
```

## Violation signals

- Silent `npm install` / `pip install`
- Only reason: “this library is popular”
- Install also rewrites unrelated version pins in the manifest

## How to tune

- **Early / toy projects**: loosen #1’s confirm; keep #2 and #3
- **Serious projects**: all four; especially never casually break #3
