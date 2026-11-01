---
type: state
status: template
read_when: Every session.
then: progress.md
---

# Project overview

<!-- Filled in by the agent during setup.md. Change `status` above to `filled` when done.
     Replace every <placeholder>. Mark anything unconfirmed as **Needs Verification**.
     Keep this under about 100 lines. It loads every session, so facts only. -->

## What this is

<Two or three sentences: what the product does, who it is for, and what problem it solves.>

**Stage:** <idea / building / live with users>

**Goals right now:** <the outcomes that matter most this month>

**Not goals:** <what this project deliberately does not try to do>

## Users and roles

| Role | Can do | Cannot do |
|---|---|---|
| <role> | <main actions> | <important limits> |

## Stack

| Layer | Choice | Version |
|---|---|---|
| Language | <value> | <value> |
| Backend | <value> | <value> |
| Frontend | <value> | <value> |
| Database and ORM | <value> | <value> |
| Hosting | <value> | <value> |

**Package manager:** <the one in use>

## Commands

These are the **check commands** the other files refer to. Keep them exact and working. Write `None` if the project has
no such command.

| Purpose | Command |
|---|---|
| Install | `<command>` |
| Run locally | `<command>` |
| Lint | `<command>` |
| Type check | `<command>` |
| Test | `<command>` |
| Build | `<command>` |
| Migrate local database | `<command>` |

## Environments

| Name | URL | Use |
|---|---|---|
| Local | <url> | Development |
| Staging | <url> | Testing |
| Production | <url> | Live. Agents never touch this. |

**Environment variables:** <names and what each is for. Names only, never values.>

## Domain words

The words the owner uses, and what they mean in the code.

| Word | Means | Found in |
|---|---|---|
| <word> | <plain meaning> | <table, module or screen> |

## Sensitive areas

<Code that needs extra care: money, permissions, data that must not be lost, anything fragile.>

## Other project docs

<Existing README, specs or policy documents in this project, and when to read each one.>
