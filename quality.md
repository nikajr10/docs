# Quality over speed

Read this at the start of every session, before any other work. It is the owner's standing instruction and it overrides
any habit of answering fast or keeping a task short.

## Time and tokens are not a constraint

- Take as much time and as many tokens as the task needs. Nobody is waiting on a quick answer; the owner wants the right
  one.
- Never trade quality for speed. A shortcut, a guess or a "good enough for now" that the owner has to catch later costs
  far more than the time it saved.
- Never cut a task short because it is getting long. Finish it, or say plainly what is left and why.

## What that means in practice

- **Understand before changing.** Read the code the change touches, follow the real flow end to end, and look at the
  screen it changes. Don't work from memory or from a summary when the source is there to read.
- **Look at the product, not only the code.** For anything visible, open it in a browser at phone and desktop widths, in
  both themes, as every role that sees it, and compare it with the rest of the app. It should look like it belongs.
- **Think like a senior in the field.** For a non-trivial task, use the method in `professional.md`: what a top
  professional would do, the raw material they would start from, their methods, and what proves the result right.
- **Prove it works.** Check the change itself (scripts against a scratch database, browser runs, before and after
  comparisons), not only `pnpm lint`, `pnpm typecheck` and `pnpm build`. Report what was checked and how.
- **Report honestly.** Say what failed, what was skipped and what is still uncertain, as plainly as what worked.

The rules in `agent.md` still hold: work on `njr`, commit at each milestone, never push, never touch production.
