# Agent instructions

Rules for any coding agent working in this repository.

## Git

- **Work on the `njr` branch.** Check with `git branch --show-current` before you start. If you are on another
  branch, switch to `njr`; never commit to `main`.
- **Commit at every milestone**, not at the end of every session or task. A milestone is a piece of work that
  stands on its own and passes the checks below: a feature or a phase of one, a fix, a migration with the code
  that uses it. Work that is half done stays uncommitted until it reaches one. Commit only what that milestone
  changed, not unrelated edits.
- **Never push.** No `git push`, no force-push, and no opening pull requests, unless the owner asks for it in so
  many words for that one time. Commits stay local until the owner pushes them.
- **Commit messages** follow the existing history: a short subject that says what changed ("Area: what changed"),
  a blank line, then a few lines on why.
- Before committing, read `git status` and `git diff --staged`. Never commit `.env` files, secrets, build output
  (`dist/`) or scratch files.
- Don't rewrite history that already exists: no `git rebase`, `git reset --hard` or `git commit --amend` on
  commits you did not just make.

## Production

- **Never touch production.** No production servers, databases, deploys or `docker-compose.prod.yml` runs. That
  includes migrations, seeds, scripts and SSH, and reading production data. Work only against local or scratch
  databases (`localhost`). Running anything in production is the owner's job.

## Before you change anything

Read `quality.md` at the start of every session: take the time and tokens a task needs, and never trade quality
for a quick answer. Then read `PROGRESS.md`: it has the project map and the owner's standing rules. For the leave and
holiday policy, read `leave-policy.md` and `holiday-implement.md`. `ARCHITECTURE.md` explains how the
code is laid out.

## Before you commit

Run `pnpm lint`, `pnpm typecheck` and `pnpm build`. They must pass. If a migration changed, also run
`pnpm db:types --verify`. Record what you checked in `PROGRESS.md`.
