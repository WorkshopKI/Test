---
name: build-from-brief
description: Take a ticket or raw idea from nothing to a verified, deployed small app using a seven-step loop (frame, gather, plan, stress-test, persist, slice, verify). Use when the user hands over a ticket, request or idea to build and wants it built in checked slices rather than one-shotted.
argument-hint: <path-to-ticket-or-idea> [ticket|idea]
allowed-tools: Read Write Edit Glob Grep Bash
---

# Build from a brief

Almost every build disaster is a framing failure: the agent did what was asked, but the ask was
wrong or was eight things at once. This loop front-loads the decisions and builds in small,
committed, verified slices.

## Input

Source document: `$0` (read it). Mode: `$1`.
- `ticket`: someone else wrote it. Use **Door B**.
- `idea`: the user wrote it. Use **Door A**.
- Empty: a request from a named person is `ticket`; the user's own idea is `idea`. Say which in one line.

If `$0` is missing or unreadable, ask for it and stop. **Never write code before `brief.md` exists on disk.**

## The loop

1. **Frame** -> write `brief.md` from [brief-template.md](brief-template.md).
   - **Door A (idea)**: one sentence with no conjunctions; name the one screen; name the user and
     the moment; write the out-of-scope list first (three real, tempting exclusions); name the
     first demoable slice (not "set up the project").
   - **Door B (ticket)**: (1) quote every noun that could mean two things and decide; (2) walk the
     edges: zero, one, a thousand, two people at once, bad input, the thing that already exists;
     (3) find the short sentence hiding the most work ("should be quick", "oh and it'd be great
     if...") and pin it to a concrete, testable rule. Every decision goes in the hidden-decisions
     table with a call and a reason. The person who wrote the ticket is usually unavailable: the
     decisions are yours now, so write them down.
2. **Gather** -> only the context this needs. For a greenfield build, almost nothing. Use real data
   the user supplied (or fetch it from a real source); never invent sample data and present it as real.
3. **Plan** -> plan mode if available. Read the plan as a contract against the brief and its
   out-of-scope list; remove anything it quietly added.
4. **Stress-test** -> run the `grill` skill (`/grill brief.md ticket`) if installed; otherwise apply
   its three passes yourself and save findings to `grill.md`. Update `brief.md` with what changed.
   Output: verdict, findings worst first, and the one thing to fix before building.
5. **Persist** -> write `plan.md` as slices, each with a "done when I can see..." line, plus a cut
   order if time runs short. Commit brief, grill notes and plan.
6. **Slice** -> one slice at a time. A slice is **visible**, **verifiable on its own**, and
   **revertible** (one commit). "The table renders three rows" is a slice; "set up the data model" is not.
   Test each slice, then `git commit -m "slice N: ..."` before starting the next. Use a
   `git worktree` only for genuinely independent slices that touch different files, and start the
   second session from inside it (check `pwd`). Merge and remove the worktree before deploying.
   If a one-shot attempt half-works, don't rescue it: revert and build the smallest visible slice.
7. **Verify** -> run it, don't read it. In a real browser (Playwright): the happy path, reload
   persistence, the empty state, bad input, and the specific behaviour the brief's "how I will
   know it worked" names. Tests Claude wrote are not verification. Finish by asking: what is the
   one thing most likely to look right and be wrong?

## Deploy

Static, browser-only app: publish it as an artifact. Otherwise use the project's deploy path
(e.g. `vercel`). Deploying is also verification: if it works locally but not deployed, a file was
never committed or something reads a local file. Push the branch.

## Hand-off

Report: what was built, how it was checked, and the decisions the ticket never made. State
limits plainly (e.g. per-browser storage, no shared data, no real data source). Do not claim
anything you did not run.
