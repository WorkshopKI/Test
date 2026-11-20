# /grill brief.md ticket  (mode: ticket — handed down from Dana)

**Verdict:** Ready to plan, once the repeat rule is pinned to one testable definition (it is, below).

## Findings (worst first)
1. **"flagged when something looks like a repeat"** — "looks like" is the sentence hiding the work.
   Same name? Same page? Same hypothesis? Those give three different flag sets: on the real data,
   name-match flags only 0046; page-match flags 0041/0042/0046 (0042 is a different metric and
   shouldn't be); hypothesis-match needs AI. *Call:* same target + same metric, normalised. Flags
   exactly 0046 → 0041. Fixed rule, no judgement. Paraphrases will be missed: accepted.
2. **"what we ran, when"** — "when" = start date, end date, or readout date. *Call:* start date only.
3. **"how it went"** — outcome label vs a number. *Call:* label + one-line note.
4. **"somewhere to see them" / two people at once** — a shared source of truth vs a per-browser
   list. Per-browser storage means two PMs see different logs: the exact failure Dana describes,
   reproduced in the tool. *Call:* ship per-browser, declare it out of scope, say so in the handoff.
   (This is the biggest remaining risk; a shared store is the first follow-up.)
5. **Edges:** zero rows (message must not imply "nothing was run"); one row (no flag possible);
   a thousand rows (no search/filter: out of scope, flagged); bad input (required fields, real
   date, `/`-prefixed target); the thing that already exists (the 8 supplied rows, seeded).
6. **Same-day duplicates** — two rows, same date, same key: who is "later"? *Call:* insertion order.
7. **"Should be quick, it's basically a list"** — the list is ~20% of the work; the rule, its
   explanation in the UI, and the live pre-save check are the rest.

## The one thing to fix before planning
Pin "repeat" to one deterministic rule and test it against the real rows. Done: see brief.md.
Expected flags on seed data: **EXP-0046 → EXP-0041 only.**
