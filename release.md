---
type: playbook
read_when: The owner asks about deploying, a release note, launch readiness, or a production problem.
then: progress.md
---

# Release and production

Deploying is the owner's job. Your job is to make it boring: a clear list of what is changing, what to run, how to check
it, and how to back out. This never overrides `agent.md`: do not touch production, and do not push unless told to.

## Step 0: Create the report file (when needed)

Create `Release-Report.md` when you prepare a release, run the launch gate or handle a production problem. Skip it otherwise.

Before doing anything else:
1. Check whether `Release-Report.md` exists in the project root.
2. If it does not exist, create it.
3. If it exists from an earlier run, clear it and write this run's report and findings into the same file. If it
   belongs to the run still in progress, carry on in it. Never create a second, dated or numbered report file.
4. Add the date, project name, branch/commit, and a one-line summary of the task at the top.

Write the results of **every step** into it as each step is completed. Do not wait until the end. Record: what is shipping, the check results, the release note, each launch gate line, and any incident timeline.

If this task already has a report from another playbook, add a section there instead of creating a second file. The rules
for reports are in `workflow.md`.

## Prepare a release

1. Find what is shipping: `git log <last release>..HEAD`, and the **Notes for next release** section of
   `progress.md`.
2. Run the check commands, including the production build, on a clean checkout if you can.
3. Check every migration in the release against `risky-changes.md`. Decide the order: does the migration run before or
   after the code deploys?
4. List new environment variables and external setup.
5. Write the release note below, and give it to the owner in your report.
6. Update the changelog and version, if the project keeps them.

## Release note

```markdown
# Release <version or date>

**What changes for users:**
- <plain words, not commit messages>

**Before deploying:**
- [ ] Back up the database
- [ ] Add env variables: <names only, never values>
- [ ] External setup: <webhooks, DNS, third-party config>

**Deploy order:**
1. <step, with the exact command>

**Check after deploying:**
- [ ] <page or endpoint> shows <result>
- [ ] Logs have no new errors

**If it goes wrong:**
- Roll back with: <exact command or steps>
- Migrations: <reversible, or what to do if not>

**Known issues:** <anything not fixed>
```

## Launch gate

Run this before a first launch, or when the owner asks if the product is ready. Report each line as PASS, FAIL or NOT
APPLICABLE with a reason.

- [ ] Check commands and the production build pass
- [ ] Main user journeys work end to end, tested in a real browser
- [ ] Every page handles loading, empty and error states, and works on a phone
- [ ] `security.md` has been run, with no open critical or high findings
- [ ] `API-Security.md` has been run, if there is an API
- [ ] `System-Test-Simulation.md` has been run, if real traffic is expected
- [ ] No secrets in code or git history. Production uses its own values.
- [ ] Rate limits exist on login and expensive endpoints
- [ ] Error tracking and logs are set up, and sensitive data is not logged
- [ ] Backups exist, and a restore has been tested
- [ ] Rollback steps are written and work
- [ ] `.env.example`, and the setup steps in `overview.md`, are correct on a clean machine

The audits are long. If one has not been run, mark that line **Needs Verification** and suggest it. Do not start one
unless the owner asked.

## When production breaks

You cannot touch production, so you work from what the owner shares, and from the code.

### 1. Stop the damage first

If users are affected now, the first question is whether to roll back. A rollback usually beats a rushed fix. Tell the
owner in one short message: what to run, and what it will do. Do not investigate first if a rollback would end it.

### 2. Understand it

- Ask for one specific thing at a time: exact error, time it started, who is affected. Do not ask for anything that
  would expose secrets, and ask them to strip personal data from logs.
- Compare the last working release against the current one with `git log` and `git diff`.
- Reproduce locally, following `debugging.md`.

### 3. Fix it

- Keep the hotfix as small as possible. No cleanup, no refactoring.
- Add a test that fails without the fix.
- Give the owner a release note, as above.

### 4. Afterwards

Add an entry to `lessons.md`:

```markdown
## L-<number>: <what broke>
**Rule:** <what must be different from now on>
**Why:** <cause, impact, and how long it lasted>
**Applies when:** <the situation in which this could recur>
```

Also add anything that should have caught this to **Next** in `progress.md`, such as a missing test or alert.
