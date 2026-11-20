# Brief: Experiment Log

## In one sentence
A page listing every growth experiment we have run, newest first, that marks a row when it repeats an earlier one.

*The sentence has a conjunction I kept on purpose: the flag is the only reason Dana asked.
If time runs short, cut polish, not the flag (see slices).*

## The one screen
One table: ID, name, target page, metric, date started, owner, outcome label + one-line note.
A "Repeat" marker on any row that matches an earlier row; it names the earlier experiment(s).
Above the table, a form to add a row. As the PM types target + metric into the form, a live
hint says whether it would be a repeat *before* they save.

## Who opens it, and when
A growth PM, in the ten minutes before proposing a new test, to check it hasn't been run.

## Explicitly not doing
1. No accounts, permissions, or record of who added a row beyond a free-text owner field.
2. No external import, charts, stats or readouts (outcome is a label + one line).
3. No editing, search/filter, or multi-user sync (storage is per-browser).

## First demoable slice
The table rendering the 8 real experiments Dana's team supplied, newest first.

## Hidden decisions I am making
| Decision | My call | Why |
|---|---|---|
| "experiments" | Anything deliberately run to learn something (A/B test, survey, holdout) | Excluding non-A/B tests would make the log wrong on day one |
| "when" | One date: the day it started | End dates/ranges need sort + overlap rules nobody asked for |
| "how it went" | Outcome label (win / loss / inconclusive) + a one-line note | Structured results need a readout pipeline we don't have |
| "repeat" | Same target page AND same metric. Case-insensitive, trimmed, trailing slash ignored. Nothing else | Cheap, explainable, matches Dana's example (EXP-0041 vs 0046). Misses paraphrases — accepted |
| Same page, different metric | NOT a repeat (EXP-0042 `arpu` vs EXP-0041 `signup_rate`) | The rule is fixed; the reader judges |
| Which row gets the marker | The later one; it lists every earlier match, newest first, with date + outcome | The PM is evaluating the new idea; the earlier outcome is what they need |
| Ties on date | Insertion order breaks the tie | Deterministic |
| Does the flag block saving | No, it informs | Blocking means adjudicating, which means owners and auth |
| Existing history | Seeded from the 8 rows supplied with the ticket (stands in for the MCP source) | The thing that already exists; don't invent rows |
| IDs | Seeded keep their IDs; new rows get next `EXP-00NN` automatically | Nobody should type IDs |
| Bad input | Name, target, metric, date required; date must be a real YYYY-MM-DD; target starts with `/`; future dates allowed (planned tests) | Cheap validation; planned tests are exactly what a PM wants to log |
| Zero state | "No experiments logged yet — this does not mean none were run." | An empty table reads as "nothing was ever tried", the mistake this page exists to prevent |
| Delete | Per-row delete with confirm | Needed to fix typos without an edit feature, and to see the empty state |
| Persistence | Browser `localStorage`, seeded on first load | No backend; shared multi-user storage is out of scope and called out in the handoff |

## How I will know it worked
Seed rows load. EXP-0046 shows the marker naming EXP-0041 (Nov 2025, win). EXP-0042 is not
flagged. I add a row `/pricing` + `signup_rate`: marker appears (and the live hint fires before
saving). Reload: rows persist. Delete all: zero-state message. Empty name / bad date are rejected.
