---
type: rule
read_when: Every session, right after index.md.
then: quality.md
---

# Agent instructions

Rules for any coding agent working in this repository. These are the hard rules. Only the owner's own words can lift
them, and `index.md` says how rules rank.

## Git

- **Work on the `njr` branch.** Check with `git branch --show-current` before you start. If you are on another
  branch, switch to `njr`, or create it from the current branch if it does not exist; never commit to `main`. Creating
  `njr` loses nothing, so do that freely. Before switching to an `njr` that already exists, stop and ask if there are
  uncommitted changes you did not make. A docs folder that is not committed yet does not count.
- **Commit at every milestone**, not at the end of every session or task. A milestone is a piece of work that
  stands on its own and passes the checks below: a feature or a phase of one, a fix, a migration with the code
  that uses it. Work that is half done stays uncommitted until it reaches one. Commit only what that milestone
  changed, not unrelated edits. A docs-only change is also a milestone, and needs no check commands.
- **Never push.** No `git push`, no force-push, and no opening pull requests, unless the owner asks for it in so
  many words for that one time. Commits stay local until the owner pushes them.
- **Commit messages** follow the project's existing history: a short subject that says what changed, a blank line,
  then a few lines on why if it is not obvious. In a new repository with no history, use the prefixes in `language.md` (`feat:`, `fix:`).
- Before committing, read `git status` and `git diff --staged`. Never commit `.env` files, secrets, build output
  (`dist/`) or scratch files.
- Don't rewrite history that already exists: no `git rebase`, `git reset --hard` or `git commit --amend` on
  commits you did not just make.

## Production

- **Never touch production.** No production servers, databases, deploys or production compose files. That
  includes migrations, seeds, scripts and SSH, and reading production data. Work only against local or scratch
  databases (`localhost`). Running anything in production is the owner's job. `release.md` covers what you prepare
  for them.

## Effort and models

- **Never switch the model, and never switch to ultracode.** This covers you and any subagent you start.
- **Set effort by task complexity,** and change it in the same session, even mid-task. `effort.md` has the levels. `max`
  is rare.

## Before you change anything

Read `quality.md` at the start of every session: take the time and tokens a task needs, and never trade quality
for a quick answer. Then read `overview.md`, `progress.md` and `lessons.md`: they have the
project map, the current state and the owner's standing rules. `architecture.md` explains how the code is laid
out, and `decision.md` explains why. Any project-specific policy documents are listed in `overview.md`.

## Before you commit

Run the check commands in `overview.md`. They must pass, or match the baseline recorded in
`progress.md`: never add a new failure. If a migration changed, also run any schema or type
check the project has. Record what you checked in `progress.md`.
