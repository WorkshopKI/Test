# Plan: Experiment Log

Single self-contained `index.html` (vanilla JS, no build) so it runs from a file and publishes
as one page. Stays inside brief.md's out-of-scope list. One commit per slice.

| # | Slice | Done when I can see |
|---|---|---|
| 1 | Table renders the 8 seeded experiments, newest first | 8 rows, outcome badges, correct dates |
| 2 | Repeat rule + marker | EXP-0046 marked, naming EXP-0041 (Nov 2025, win). Nothing else marked |
| 3 | Add form: validation, auto ID, live pre-save repeat hint, localStorage persistence | Add `/pricing` + `signup_rate` -> hint + marker; reload keeps it; bad input rejected |
| 4 | Delete row + zero state | Delete all -> "No experiments logged yet — this does not mean none were run." |
| 5 | Verify in a real browser (Playwright), then publish as artifact | Checks from brief pass; link delivered |

Cut order if short on time: 4's delete confirm, then 3's live hint. Never the marker.

Repeat rule (single function `repeatsOf(row, rows)`): key = trim+lowercase target with trailing
slash stripped (except "/"), plus trim+lowercase metric. Earlier = strictly earlier date, or same
date and earlier insertion. Returns all matches newest first.
