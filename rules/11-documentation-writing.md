# 11 · Documentation writing (P1*)

**English** | [简体中文](11-文档写作.md)

> \* Day-to-day: P1. When docs are the main deliverable: treat as **P0**. Cheat-sheets may skip tone clauses (sections 1–7 style rules); governance clauses still apply.

Use this to constrain first-draft project docs. The default AI failure mode is writing for **people who already know the answer** — treating output as a memory index, not an explanation. Every clause below fights that.

---

## 1. Principles

1. **Reader model**: someone three months from now (including you), a colleague who missed every discussion, or a stranger. Anything that only lived in chat must be re-explained.
2. **Docs explain; they are not indexes**: body text uses full sentences. Tables/lists support prose — they do not replace it.
3. **Concrete before abstract**: ground every principle in a project-specific example first. No floating jargon.

---

## 2. Language rules

| # | Rule | Bad | Better |
|---|------|-----|--------|
| L1 | **No telegram style**: subject, predicate, connectives (because / so / e.g. / otherwise / this means) | "don't void decision history; don't phase the build sheet" | Full sentences explaining what git owns vs what the doc owns and why |
| L2 | **Term trio** on first use: plain definition + project example + why it matters | "Contract: which log fields?" | Define the handoff, give three fields, explain independent evolution |
| L3 | **Cause pairs**: what + why; never conclusion alone | "Fail: expose bad data early" | Strategy + reason (false negatives vs false positives) |
| L4 | **One new idea per sentence** | Stacked abstractions in one line | Split into two sentences |
| L5 | **Open with a real reader question**, then answer | "Three layers; don't mix" | Why separate run / decision / product layers |
| L6 | **Helpful redundancy OK**: key conclusions may repeat once in prose and a table |
| L7 | **Register metaphors**: bind ("translator", "ladder") to the formal concept on first use |

### L4 rewrite example

Bad: "Above the runtime layer train the decision layer, then abstract into product decomposition."

Better: "This guide climbs two steps: from what this line does (runtime) to why it was designed that way (decision); then turns that design thinking into reusable steps for splitting a new product."

---

## 3. Structure rules

| # | Rule | Note |
|---|------|------|
| S1 | **Three-question open**: what is this? when do I need it? what can I do after? | Full sentences |
| S2 | **Reading paths** by reader role — not a bare file list | "Use it → A→B; change it → C→D; learn → start at E" |
| S3 | **"See xxx" cannot be the only explanation** | Link after a self-contained minimum |
| S4 | **Every summary row implies a full explanation** elsewhere in the same doc | |
| S5 | **No bare meta titles** ("Boundary", "Shape") — add the scene | |

---

## 4. Ban list (paste into prompts)

- Abstract meta-words as titles/body with zero explanation
- Three+ consecutive lines without a full sentence
- Tables with no surrounding prose explaining what they are and how to read them
- Chains of impersonal commands ("Dictate: inputs/outputs/branch kinds")
- Chat-only abbreviations and code-words dropped into docs
- Links used as a substitute for explanation
- Conclusion paragraphs with no reason

---

## 5. Governance (what to write / not write)

Complements tone rules. Clause 7 can be a hard permission (main agent only writes the docs library).

1. Describe **current** state only — no AI change diaries in docs or comments.
2. Unconfirmed plans (e.g. phase1–5) do not become doc fields.
3. When decision B replaces A, write B and erase A — readers should not sort history vs current.
4. Docs describe architecture, not implementation; point to where code lives.
5. Docs are not changelogs — git owns history.
6. Keep a single nav (`docs/README.md`); register new docs before they exist as orphans.
7. Sub-agents implementing code must not edit the docs library; they propose; the main agent decides and dispatches writes.

---

## 6. Pre-submit checklist (agent must self-check)

1. Hide bold and tables — can a cold reader understand the prose?
2. Can someone who knows the project but missed discussions name the topic in 30 seconds from paragraph one?
3. Every new term: definition, example, reason on first use?
4. Every summary row has a full explanation in body text?
5. Any sentence a reader would ask “what does this mean?” with no answer?
6. Any 3+ lines without a full sentence?

Fail any item → revise before delivery.

---

## 7. Prompt template (copy-paste)

```text
Write a [tutorial / architecture note / user guide / learning note] for project [NAME].

Reader: knows the rough goal, joined none of the discussions, remembers none of the
chat abbreviations, metaphors, or decision background. Future-you in three months
is also in scope.

Writing:
1. Full sentences only — no telegram fragments as body text.
2. New abstractions: plain definition → project example → why it matters; one new idea per sentence.
3. Every rule/decision: what + why.
4. Open each section with a real reader question, then answer.
5. Prose before/after every table or list; key conclusions may repeat once.
6. Nav content must give reading order by role — not a bare file list.

Governance:
1. Current state only — no history of edits or AI action logs.
2. No unconfirmed phase plans in the doc.
3. Replaced decisions: write the new one; delete the old wording entirely.
4. Architecture, not implementation — code is source of truth; docs point the way.
5. Not a changelog; git owns history.
6. If docs/README.md nav is affected, update it in the same change.

Banned:
- Bare meta titles/body (boundary/contract/shape/failure/…)
- 3+ lines without a full sentence
- "See link" as the only explanation
- Chat-only code-words, abbreviations, metaphors without registration

Self-check before delivery (fix any → revise):
□ Prose alone is readable
□ Topic clear in 30s from paragraph one
□ Terms have definition, example, reason
□ Summaries have full body counterparts
□ No 3+ sentence-less lines
□ No obsolete decisions / unconfirmed phases / edit diaries
□ Nav table synced if docs were added/renamed/removed
```

---

## Why this works

Unreadable AI docs usually fail on **goal**, not talent: maximizing information density (cheatsheets, release notes, design scraps) for people who just left the meeting. You need readers three months later — or strangers.

Good human tutorials simulate a reader asking “do I get this? why? example?” after every sentence. This rule forces that simulation.
