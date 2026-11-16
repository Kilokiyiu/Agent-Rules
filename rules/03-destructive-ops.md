# 03 · Destructive operations (P0)

[简体中文](03-破坏性操作.md) | **English**

Irreversible actions (delete files, reset branches, wipe data) require: inventory → confirm → then execute.

## Why this rule

Prompts are soft; agents “forget” in long context. Deleted files do not. This is the one rule that should land in **both** prompts and tool permissions — prompts remind, permissions enforce. Confirm-before-delete that lives only in a prompt decays badly in long chats.

## When to use

Any filesystem, git, or database work. These always need the confirm flow:

- Delete or overwrite any file (including bulk rename / empty a directory)
- `git reset --hard` / `git push --force` / discard working-tree changes
- Schema changes or truncating tables
- Overwriting config files the user did not ask to change

## Prompt (copy-paste)

```text
[Destructive operations]
The following are high-risk. Before acting: list every affected object, state the
risk, and wait for an explicit user "confirm/agree":
- Delete or overwrite any file (including bulk rename / emptying directories)
- git reset --hard / git push --force / discard working-tree changes
- DB schema changes or truncating tables
- Overwriting config the user did not ask to change
- Anything that is not easily undone
If the user refuses, do not retry the same intent in another form.
```

## Violation signals

- “Also cleaned temp files” with no prior list
- After refusal, same intent via another command (`rm` → `find -delete`)
- “Reset the workspace” without naming uncommitted loss

## Hard config suggestion

```text
# Second gate in project agent permissions (beyond prompts)
- rm/del style deletes: require confirm
- git reset --hard / push --force / history rewrite: require confirm
- Bulk ops (>10 files move/rename/delete): require confirm and batch (≤10 each)
```
