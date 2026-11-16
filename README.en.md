<div align="center">

# Agent Rules

[简体中文](README.md) | **English**

**Make your agent follow your habits**

Change only what you asked · Report only what actually happened · Ask before anything destructive

<br/>

![Rules](https://img.shields.io/badge/rules-11_dimensions-0F172A?style=flat-square)
![P0](https://img.shields.io/badge/P0-always_on-DC2626?style=flat-square)
![P1](https://img.shields.io/badge/P1-serious_projects-D97706?style=flat-square)
![P2](https://img.shields.io/badge/P2-opt_in-16A34A?style=flat-square)
![Copy-paste](https://img.shields.io/badge/usage-copy--paste-2563EB?style=flat-square)

<br/>

[Rules hub](rules/README.en.md) · [Copy-paste prompts](docs/AGENTS.en.md) · [Docs writing](rules/11-documentation-writing.md)

</div>

---

Most AI coding failures are not about weak models — they are about **agents you cannot control**. They refactor behind your back, invent “tests passed” stories, delete files without asking, or quietly add dependencies.

This repo splits those failure modes into **11 copy-paste constraints** so the agent does what you asked:

| Soft constraints | Hard gates |
|:----------------:|:----------:|
| Dimensioned prompts you can mix<br/>and paste into a chat or project config | File permissions and high-risk confirms<br/>wired into Agent / tool settings |

Works with Cursor, Claude Code, and any agent that supports `AGENTS.md` / system prompts.

Every rule page is bilingual: **简体中文** (default) · English counterparts (`README.en.md`, `*-*.md` English filenames).

---

## Contents

| | |
|---|---|
| 01 | [Why these rules](#1-why-these-rules) |
| 02 | [Quick start](#2-quick-start) |
| — | [Prompt pack](#prompt-pack) |
| 03 | [Rule index](#3-rule-index) |
| 04 | [How to combine them](#4-how-to-combine-them) |
| 05 | [Hard permission layer](#5-hard-permission-layer) |
| 06 | [Repo layout](#6-repo-layout) |
| 07 | [How to iterate](#7-how-to-iterate) |

---

## 1. Why these rules

> Every rule page follows the same shape: **why → when → copy-paste prompt → violation signals → how to loosen/tighten**

| Common failure | Which rule |
|----------------|------------|
| You asked for a bugfix; it refactored the whole module | [01 · Scope control](rules/01-scope-control.md) |
| It says “tests passed” — and may never have run them | [02 · Honesty](rules/02-honesty.md) |
| Deletes files / force-pushes without confirmation | [03 · Destructive ops](rules/03-destructive-ops.md) |
| Installs packages or swaps frameworks without asking | [04 · Dependency management](rules/04-dependency-management.md) |
| Wrong direction discovered only after a pile of rework | [05 · Plan first](rules/05-plan-first.md) |
| Deletes tests to make the suite “green” | [06 · Test verification](rules/06-test-verification.md) |
| New code looks like a different style guide | [07 · Style consistency](rules/07-style-consistency.md) |
| Commits on its own with message `update` | [08 · Git hygiene](rules/08-git-hygiene.md) |
| Secrets in source, string-built SQL | [09 · Security floor](rules/09-security-floor.md) |
| Adds a button and restyles the whole site | [10 · Frontend constraints](rules/10-frontend-constraints.md) |
| Docs read like telegram fragments | [11 · Documentation writing](rules/11-documentation-writing.md) |

Full navigation and the combined prompt pack → **[rules/README.en.md](rules/README.en.md)**

---

## 2. Quick start

### Option A · Project-level (recommended)

Copy the combined prompt pack into any of:

```text
CLAUDE.md
AGENTS.md
.cursor/rules/
```

Ready-to-copy files:

```text
docs/AGENTS.md       ← 简体中文 (default)
docs/AGENTS.en.md    ← English
```

### Option B · Paste per chat

For small tasks, paste the **P0 trio** (`01` / `02` / `03`), then add one more by scenario:

```text
UI change        →  add  10 · Frontend
Bug fix          →  add  06 · Tests
Writing docs     →  use  11 · prompt template at end of that rule
New dependency   →  add  04 · Dependencies
Medium/large work→  add  05 · Plan first
```

### Prompt pack

→ **[rules/README.en.md · combined prompts](rules/README.en.md#combined-prompt-pack-copy-paste)**  
→ [docs/AGENTS.en.md](docs/AGENTS.en.md) · [docs/AGENTS.md](docs/AGENTS.md)

---

## 3. Rule index

```text
🔴 P0  Always on              Scope · Honesty · Destructive ops
🟡 P1  Recommended for real work  Deps · Plan · Tests · Style · Docs
🟢 P2  Opt in by project type     Git · Security · Frontend
```

| # | Rule | Priority | One-liner |
|:-:|------|:--------:|-----------|
| 01 | [Scope control](rules/01-scope-control.md) | 🔴 **P0** | Only what you asked — not what it thinks is “also worth doing” |
| 02 | [Honesty](rules/02-honesty.md) | 🔴 **P0** | Separate “I know” from “I guess”; report only real outcomes |
| 03 | [Destructive ops](rules/03-destructive-ops.md) | 🔴 **P0** | Delete / reset / wipe data: list → confirm → then act |
| 04 | [Dependency management](rules/04-dependency-management.md) | 🟡 **P1** | Before any new package: reason + your OK |
| 05 | [Plan first](rules/05-plan-first.md) | 🟡 **P1** | Medium/large changes: plan first, execute after confirm |
| 06 | [Test verification](rules/06-test-verification.md) | 🟡 **P1** | Changes need real verification; no fake greens |
| 07 | [Style consistency](rules/07-style-consistency.md) | 🟡 **P1** | New code should match *your* repo style |
| 08 | [Git hygiene](rules/08-git-hygiene.md) | 🟢 **P2** | Commits only with your OK; clean diff; clear why |
| 09 | [Security floor](rules/09-security-floor.md) | 🟢 **P2** | No secrets in source · validate input · parameterized SQL |
| 10 | [Frontend constraints](rules/10-frontend-constraints.md) | 🟢 **P2** | Follow the existing design system; no freestyle redesigns |
| 11 | [Documentation writing](rules/11-documentation-writing.md) | 🟡 **P1\*** | Write docs humans can actually read |

<sup>\*</sup> When docs are the main deliverable, treat rule 11 as **P0**. Cheat-sheets may skip tone clauses — see that rule for details.

---

## 4. How to combine them

Tune by project stage — do not enable everything forever.

| Situation | How to tune |
|-----------|-------------|
| **Early prototype** | Pause `05` for speed; loosen dependency confirms |
| **Refactor / near ship** | Keep `05` on; tighten scope and style |
| **Multi-agent** | `01` + `03` + [permissions](#5-hard-permission-layer) are mandatory |
| **CLI with no UI** | Skip `10` |
| **Offline personal scripts** | Skip `09` if you want |
| **Docs-heavy work** | Promote `11` to P0; use its template |

<details>
<summary><b>Multi-agent note</b></summary>

<br/>

Sub-agents stepping on each other is the top failure mode in multi-agent setups. Enable at least:

1. [01 · Scope control](rules/01-scope-control.md) — stop out-of-scope edits  
2. [03 · Destructive ops](rules/03-destructive-ops.md) — stop irreversible actions  
3. Hard permissions below — sub-agents must not write the docs library / `.git/` directly

</details>

---

## 5. Hard permission layer

> Prompts are reminders. Permissions are gates. “Ask before delete” that lives only in a prompt decays badly in long chats.

```text
# ── File permissions ────────────────────────
- Deny sub-agent writes to: docs/, reference/, lessons/, .git/
- Sub-agents may only report findings as suggestions to the main agent
- Doc writes and commits are done or dispatched by the main agent only

# ── High-risk ops (confirmation required) ───
- rm / del style deletes
- git reset --hard / push --force / history rewrites
- Bulk ops (>10 files moved / renamed / deleted): confirm and batch

# ── Floor ───────────────────────────────────
- These are hard boundaries; no prompt may be read as permission to bypass them
```

Full notes and the combined prompt → **[rules/README.en.md](rules/README.en.md)**

---

## 6. Repo layout

```text
Agent Rules/
│
├── README.md                         ← 简体中文 (default)
├── README.en.md                      ← English (this page)
│
├── rules/
│   ├── README.md                     ← Chinese hub
│   ├── README.en.md                  ← English hub
│   ├── 01-范围控制.md                🔴 P0  (+ 01-scope-control.md)
│   ├── 02-诚实性.md                  🔴 P0
│   ├── 03-破坏性操作.md              🔴 P0
│   ├── 04-依赖管理.md                🟡 P1
│   ├── 05-计划先行.md                🟡 P1
│   ├── 06-测试验证.md                🟡 P1
│   ├── 07-风格一致性.md              🟡 P1
│   ├── 08-git规范.md                 🟢 P2
│   ├── 09-安全底线.md                🟢 P2
│   ├── 10-前端约束.md                🟢 P2
│   └── 11-文档写作.md                🟡 P1
│
└── docs/
    ├── AGENTS.md                     ← Chinese prompt pack (default)
    └── AGENTS.en.md                  ← English prompt pack
```

Each rule page links to its language twin at the top.

---

## 7. How to iterate

This is v1 and still evolving.

Whenever an agent violates a rule, paste the exact quote into that rule’s “violation signals” section. Accumulated samples tell you what to tighten and what to relax.

---

<div align="center">

Issues / PRs welcome: real violation quotes, loosen/tighten suggestions, or adapters for other agent tools.  
Use the **Violation sample** or **Rule improvement** issue templates.

<br/>

**[Start here → rules/README.en.md](rules/README.en.md)** · **[简体中文](README.md)**

</div>
