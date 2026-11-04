---
type: playbook
read_when: A change touches the database, a public API, dependencies, config, or deletes or moves a lot of code.
then: Return to the step of workflow.md you came from.
---

# Risky changes

Most changes can be undone by reverting a commit. The ones in this file cannot, or they break something outside the
code you can see. Slow down for these, and leave a way back.

## Step 0: Create the report file (when needed)

Create `Risky-Changes-Report.md` when the change is in the "ask the owner first" column below, or a migration changes existing data. Skip it otherwise.

Before doing anything else:
1. Check whether `Risky-Changes-Report.md` exists in the project root.
2. If it does not exist, create it.
3. If it exists from an earlier run, clear it and write this run's report and findings into the same file. If it
   belongs to the run still in progress, carry on in it. Never create a second, dated or numbered report file.
4. Add the date, project name, branch/commit, and a one-line summary of the task at the top.

Write the results of **every step** into it as each step is completed. Do not wait until the end. Record: what changed and why, the way back, the proof, and what the deploy must do.

If this task already has a report from another playbook, add a section there instead of creating a second file. The rules
for reports are in `workflow.md`.

## Do it, or ask first

| Change | Do it with care | Ask the owner first |
|---|---|---|
| Database | Add a table, add a nullable column, add an index | Drop or rename a column or table, change a type, delete or rewrite data |
| API | Add an endpoint or an optional field, or tighten a permission check to close a hole | Remove or rename a field, change a meaning, change what clients must do to log in |
| Dependencies | Add a small one that follows the rules below, or a patch or minor upgrade | Major upgrade, new framework, ORM or database, a paid service |
| Config | Add an env variable with a safe default | Add a required env variable, change CORS, auth or infrastructure |
| Code | Delete code you have proven unused | Delete a feature, or a large rewrite |
| Git | Commit on the working branch | Anything that rewrites history |
| Money or external | Use sandbox keys and test mode | Anything that sends real email or SMS, or charges money |

If the owner's prompt asks for that exact change, that is approval, so do not ask again. When you do ask, include what you
recommend and how you would undo it.

## Every risky change needs

1. **A reason.** Add an entry to `decision.md` when you chose between real options.
2. **A way back.** Know how to undo it before you start.
3. **Proof.** Test on a scratch copy, not on data that matters.
4. **A note.** Add anything the deploy must do to `progress.md`, for `release.md`.

## Database migrations

Never touch a production database. Migrations run locally, and on a scratch database, and the owner runs them in
production.

- Change the schema only through migrations. Never by hand.
- Do not edit a migration that has already been applied or merged. Write a new one.
- Include a working rollback, or say plainly that it cannot be rolled back.
- Run it up, check the result, run it down, and run it up again.
- Think about the old rows. A rule that holds for new data often fails on old data.
- A column added as `NOT NULL` with no default fails on a table that already has rows.
- On large tables, some operations lock the table. Add indexes concurrently where the database supports it, and flag
  long operations to the owner.

### Change the shape safely

Do not rename or remove something in one step. The running app and the new schema must work together during a deploy.
Use expand, migrate, contract:

1. **Expand.** Add the new column or table. Keep the old one.
2. **Write both.** The app writes to old and new.
3. **Backfill.** Copy old data across in small batches, safely re-runnable.
4. **Read new.** Switch reads, and check the data.
5. **Contract.** In a later release, stop writing the old one and remove it.

### Rewriting data

- Back up first, and make that step the owner's job in production.
- Write the script so it can run twice with no harm.
- Run a dry run that reports what it would change.
- Check the row counts before and after.

## API changes

Anything another client depends on is a contract: frontend, mobile app, third parties, webhooks.

- Adding is safe. Removing or changing is not.
- Search for every consumer before you change a response shape. Mobile apps on old versions cannot be updated at the
  moment you deploy.
- If a break is needed, version it (`/api/v2`), or support both shapes for a while.
- Update API docs, shared types and the frontend in the same change.
- Follow the API contract in `language.md`.

## Dependencies

Before adding a package, confirm all of these:

- Nothing in the project, the standard library or the platform already does this.
- It is more than a few lines' worth of value.
- It is the real package: check the exact name, publisher, recent releases and download numbers.
- It is maintained, its licence fits, and it has no serious known vulnerabilities.
- You use the project's package manager, and only one lockfile changes.

After adding, say why in your report. To upgrade, read the changelog for breaking changes, upgrade one thing at a time,
and run the check commands after each.

## Config and environment

- Add every new variable to `.env.example`, and to the list in `overview.md`.
- Validate it at startup, so a missing value fails early.
- Tell the owner about any new production value, in `progress.md`, for `release.md`.

## Deleting and moving code

- Prove that it is unused. Search for dynamic use too: string names, reflection, routes, cron jobs, config, tests and
  other repositories.
- Delete in its own commit, so it is easy to revert.
- Keep moves and renames apart from behaviour changes, so the diff can be read.
- For files you did not create, look at what is in them before you delete or overwrite them.

## Things to never do

Unless the owner says so in so many words, for that one time:

- Run anything against production.
- Run `DROP`, `TRUNCATE` or a `DELETE` without a `WHERE` on a database that matters.
- Rewrite shared git history, or force-push.
- Run `rm -rf` outside folders you created for this task.
- Disable auth, CORS, TLS or a test to get past a problem.
- Send real emails, SMS or charges during testing.
