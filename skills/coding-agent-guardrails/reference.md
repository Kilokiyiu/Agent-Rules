# Coding Agent Guardrails — Reference

Companion to [SKILL.md](SKILL.md). Read this when installing, tuning, or wiring hard permissions.

## Why these rules exist

Most AI coding failures are control failures, not model failures: drive-by refactors, invented “tests passed,” deletes without asking, silent dependency installs. These 11 constraints turn those modes into enforceable habits.

Works with Cursor, Claude Code, Copilot, and any agent that supports `AGENTS.md` / system prompts / skills.

## Rule index

| # | Rule | Priority | One-liner |
|:-:|------|:--------:|-----------|
| 01 | Scope control | P0 | Only what was asked — not “also worth doing” |
| 02 | Honesty | P0 | Separate know vs guess; report only real outcomes |
| 03 | Destructive ops | P0 | Delete / reset / wipe: list → confirm → act |
| 04 | Dependency management | P1 | Justify + confirm + pin; prefer stdlib/existing |
| 05 | Plan first | P1 | Multi-file or ambiguous → plan then act |
| 06 | Test verification | P1 | Real output; never delete/skip tests to go green |
| 07 | Style consistency | P1 | Mirror this repo, not generic “best practice” |
| 08 | Git hygiene | P2 | No commit/push/merge without OK |
| 09 | Security floor | P2 | Secrets, input validation, parameterized SQL |
| 10 | Frontend constraints | P2 | Tokens and existing libraries only |
| 11 | Documentation writing | P1* | Full sentences, what+why, current state only |

\* Promote to P0 when docs are the main deliverable.

## Combine by stage

| Stage | Keep | May loosen |
|-------|------|------------|
| Prototype / spike | P0 (all) | Plan first; some P1 style rigidity |
| Active feature work | P0 + Deps + Plan + Tests + Style | Frontend/Security if N/A |
| Near ship / multi-agent | All relevant + hard gates | None of P0; Honesty and Test #4 never loosen |
| Docs-only | Scope + Honesty + Docs (as P0) | Frontend |

**Never loosen:** Honesty (all), Test verification #4 (no delete/skip tests to green), Destructive ops confirmation after refusal.

## Hard permission layer

Prompts decay in long chats. Put this in project agent config / tool permissions:

```text
# File permissions
- Deny sub-agent writes to: docs/, reference/, lessons/, .git/
- Sub-agents may only report findings as suggestions to the main agent
- Doc writes and commits are done or dispatched by the main agent only

# High-risk ops (cannot skip)
- rm/del style deletes: require confirm
- git reset --hard / push --force / history rewrite: require confirm
- Bulk ops (>10 files move/rename/delete): confirm and batch (≤10 each)

# Floor
- These are hard boundaries; no prompt may be read as permission to bypass them
```

## Violation signals (tune from real quotes)

Paste real agent quotes into your project notes when a rule fails:

| Rule | Typical signal |
|------|----------------|
| Scope | Diff touches unmentioned files; “also cleaned up…” |
| Honesty | “Tests passed” with no output; unsourced latency/accuracy |
| Destructive | Silent temp cleanup; retry after refuse via another command |
| Deps | Surprise `package.json` / lockfile churn |
| Plan | Large rewrite without a confirmed plan |
| Tests | Deleted or skipped failing tests |
| Style | New patterns that match no sibling file |
| Git | Unsolicited commit / vague message `update` |
| Security | Hard-coded token; string-built SQL |
| Frontend | Freestyle colors; swapped UI library |
| Docs | Telegram fragments; AI edit diaries; unconfirmed phase plans |

## Install paths

| Target | Action |
|--------|--------|
| Skill install | Keep this folder as `coding-agent-guardrails/` with `SKILL.md` |
| Project prompts (中文) | Copy [prompts.zh.md](prompts.zh.md) → `AGENTS.md` / `CLAUDE.md` / `.cursor/rules/` |
| Project prompts (English) | Copy [prompts.en.md](prompts.en.md) → same destinations |
| Chat paste | Paste P0 from SKILL.md; add scenario rows from Quick scenario add-ons |

Upstream source repo may also ship the same packs under `docs/AGENTS.md` and `docs/AGENTS.en.md`.

## License

MIT — Copyright (c) 2026 Kilokiyiu. Commercial packaging and sale are allowed; retain the copyright and permission notice in distributed copies. See [LICENSE](LICENSE).
