---
type: rule
read_when: At the start of every task, and whenever a task turns out harder or easier than expected.
then: workflow.md
---

# Effort

Effort is how deeply you think, not how carefully you work. Match it to the difficulty of the work in front of you, and
change it as that difficulty changes. Too little causes confident mistakes. Too much wastes time and tokens on work that
never needed it.

## The three rules that never bend

1. **Never switch the model.** Stay on the model the session started with, for the whole session. This applies to you
   and to any subagent you start.
2. **Never switch to ultracode.** Not for a hard task, and not if you think it would help.
3. **Stay in the same session.** Switching effort never means starting a new session. Keep the context you have built up,
   even when the switch happens in the middle of a task.

If a task seems to need a different model or ultracode, do the best you can at `high`, or `max` if it qualifies, and tell
the owner what is holding you back. Only the owner can lift these rules, in so many words, for that one time. If the
model is unavailable, stop and report it. Do not fall back to another one.

## The levels

Use these four levels only.

| Level | Use it for | Examples |
|---|---|---|
| **low** | Mechanical work with one obvious answer | Fix a typo, change text or a color, rename across files, run a command, look something up, answer a simple question |
| **medium** | Normal work with a clear path. This is the default. | Add a field through the layers, build a screen from an existing pattern, fix a bug whose cause is easy to find, write tests for clear logic |
| **high** | Work that needs real reasoning, or where a mistake is costly | A bug with an unclear cause, a change across several modules, design choices, anything touching auth, permissions, money, migrations or personal data |
| **max** | Rare. Almost never. | See below |

## Choosing the starting level

Start from the task size in `workflow.md`, then raise it if a line below applies.

| Size | Start at |
|---|---|
| Small | low |
| Medium | medium |
| Large | high |

**Raise to at least high when:**

- The task touches anything in `secure-coding.md` or `risky-changes.md`.
- A wrong answer would be hard to notice, such as a calculation or a permission check.
- You do not yet understand why something is happening.

Any doubt between two levels goes to the higher one.

## When max is allowed

`max` is for the rare case where `high` was not enough. Before you use it, all of these must be true:

- You worked at `high` and it did not solve the problem, or the problem clearly goes beyond it.
- What is missing is depth of reasoning, not information. If you need to read more code, run more tests or gather more
  evidence, do that instead. `max` will not replace evidence you do not have.
- The problem is worth it: a subtle race condition, a data-integrity bug, or a security or money design that cannot be
  safely tested first.

Use it for that one problem only, then drop back down straight away. Most projects should go a long time without it.

## Switching during a task

Effort belongs to the current piece of work, not to the whole task. One task will often pass through several levels:

| Part of the task | Level |
|---|---|
| Work out the cause of the bug and design the fix | high |
| Build the fix across the files | medium |
| Run the checks, update the project files and write your report | low |

**Move up when:**

- The same approach has failed twice.
- The change reaches further than you expected.
- You find it touches something from the "raise to at least high" list.
- You are about to make a choice that is hard to undo.

**Move down when:**

- The hard thinking is finished and what is left is mechanical.
- The task turned out simpler than it looked.

Do not ask permission for any of this. Switch, and carry on.

## How to switch

**Moving down:** if you cannot change your own level, carry on at the current one. Never stop, ask or start a subagent
just to lower effort. A higher level only costs tokens, and that costs less than interrupting the owner.

**Moving up:** use the first of these that works in your tool:

1. **You can change your own effort.** Change it and carry on.
2. **You can start a subagent with its own effort.** Give that piece of work to a subagent at the level it needs. This
   stays in the same session and needs nothing from the owner.
   - In Claude Code, use the Agent tool's `effort` setting. Do not set `model`, and do not use the `fork` type, because
     it ignores `effort`.
   - Use only agent types that run on the session's model.
   - Give it a complete brief, because it knows only what you tell it. Review what it returns before you trust it.
3. **Only the owner can change it.** In Claude Code, session effort is changed by the owner typing `/effort`, and you cannot
   do this yourself. If the higher level matters, finish what does not depend on it, then end your reply with one line,
   for example: `Switch needed: type /effort high, then continue. Reason: the cause is still unclear after two attempts.`

Do not edit settings files to change effort. In Claude Code they only apply from the next session, which breaks the rule
of staying in the same session.

## What effort never changes

Lower effort is never a reason to lower the bar:

- `quality.md` and `agent.md` apply at every level.
- `verification.md` is required at every level. A `low` task still gets checked.
- Security rules and data safety do not relax for a task that looks small.

## Telling the owner

When you switched level, add one line to your report: the level, and why. For example: `Effort: medium, then high for the
migration.` Do not narrate each switch as you go.
