# Pilot log

**Started** 7 Sep 2026
**What this is** Running observations from real use of the delivery page. One entry per delivery, plus a standing tally.

This file exists because the brief holds *decisions and assumptions*, not observations, and stuffing every measurement into it would bloat the document that other sessions read first. Five things need evidence over time — `A-01` expiry, `A-02`/`A-03` cadence, `A-08` marking done, `A-09` hide-to-keep, `A-10` the calendar channel — plus the `D-15` clock and the three secondary diagnostics. They accrue here.

**Rule carried from `D-16`:** everything recorded here comes from gestures Barbara makes for her own reasons. Nothing in this log may justify adding a control to the page.

---

## Standing tally, as of 7 Sep 2026

| Measure | Value | What it bears on |
|---|---|---|
| Items surfaced | 10 (two deliveries) | — |
| Kept | 7 | keep rate |
| **Keep rate** | **~70%** | **`D-18` assumed 20–40%** |
| Hidden ("less like this") | 0 | `A-09` |
| Hide-to-keep ratio | 0 : 7 | `A-09` tripwire |
| Marked done | 0 | `A-08` |
| Median keep → done | not yet measurable | `D-15` needs 3 completions |
| Expired unkept | 0 (first window closes 16 Sep) | `A-01` |
| Shelf occupancy | **7 of 7 — full** | `D-08` |

---

## The finding that matters so far

**The keep rate is roughly 70%, against the 20–40% `D-18` assumed, and the shelf filled on day one.**

`D-18`'s arithmetic was: 5 items × 20–40% keep = 1–2 keeps per delivery, which a 7-slot shelf absorbs while roughly two items get finished per fortnight. At 70%, five items produce ~3.5 keeps per delivery. At weekly cadence that saturates any shelf size within a fortnight and holds it saturated unless ~3.5 items are finished per week.

So the number that is wrong is not necessarily the cap. Three readings are live, and one delivery cannot separate them:

1. **The picks are genuinely good** and the delivery should be smaller — 3 twice-weekly rather than 5 weekly — so the keep count per cycle falls back into range.
2. **The bar for keeping is too low**, because Delivery 001 gave no way to judge an item without opening Gmail. "Keep" did the work of *deal with this later*, which is the read-it-later failure mode in `F-03`. Delivery 002 is the first where the text can be skimmed before committing, so the next cycle discriminates between this reading and the first.
3. **Both.**

**Do not resolve this from one data point.** Barbara elected on 7 Sep to hold both caps fixed (5 and 7) and gather another cycle, which is the right call: changing two numbers against n=10 would destroy the ability to attribute any change.

### Caveats on the 70%

- n = 10 items across two deliveries **one day apart**. This is not a steady state; Delivery 002 arrived before 001 had aged at all.
- Delivery 001's links open Gmail (it predates `D-22`), so keeping may have substituted for judging.
- Three of Delivery 002's five items are partly paywalled, so the shelf holds openings rather than whole articles for those.

### Immediate consequence

The shelf is full, so **Keep is disabled on every live Lane A item**. Delivery 002's items clear on 17 Sep. If nothing is finished or removed before then, they go unkept — which is the `D-08` forcing function working as specified ("adding past the cap requires removing something first"), and the resulting loss is itself evidence for `A-01`.

---

## Delivery 001 — surfaced 6 Sep 2026

| | |
|---|---|
| Window | 31 Aug – 6 Sep · clears 16 Sep |
| Drawn from | ~202 candidates |
| Surfaced | 5 |
| Links | Gmail thread ids — **predates `D-22`** |
| Article text on shelf | none |

Built the same day the page was, and hours before `D-22` was ratified. Recorded as a partial pilot, not as a delivery that satisfies the decision.

## Delivery 002 — surfaced 7 Sep 2026 (Monday)

| | |
|---|---|
| Window | 6 – 7 Sep · clears 17 Sep |
| Field-adjacent candidates | 14 |
| Surfaced | 5 · dropped 9 |
| Links | canonical article URLs, except HackerNoon |
| Article text on shelf | 4 of 5 |

**First delivery under `D-22`.** Selection rule applied: one item per source, balanced across the three fields, so a prolific week cannot take two slots.

Short window (two days) because the project moved to build-test-iterate rather than waiting for a clean seven-day sample. Recorded so the small candidate pool is not mistaken for a quiet week.

### What `D-22` actually delivers, measured

Worth keeping because these are properties of her sources, not of the implementation:

- **Full text:** Juan Sequeda. Free publication, complete article in the email.
- **Opening section only:** Ken Huang, Beyond Euclid, Nate's Newsletter. All paywalled partway. The shelf marks where the free portion ends.
- **No text and no canonical link:** HackerNoon. Its digest publishes only per-subscriber tracking redirects, never a plain article URL. Embedding one would put a tracking token identifying Barbara into the page, so that item falls back to Gmail.

So `D-22` is **partly satisfiable, not fully**, and the ceiling is set by the publishers. Roughly one item in five will carry whole text; most carry an opening; some carry none. This is a real constraint on how much "the reading arrives where the commitment is" can ever be true, and it should inform any later decision about paid subscriptions or full-text fetching.

---

## Arrival channel

**Calendar event created by hand, 7 Sep 2026** — `D-20` satisfied, and `A-10` can now start being tested.

| | |
|---|---|
| Title | Current-Depth Review Time! |
| Recurrence | Weekly on Monday **and** weekly on Wednesday, 8:00pm CT |
| Carries | the stable artifact link, in the description |
| Created by | Barbara, by hand. Nothing automated touches the calendar. |

**Two events, two jobs.** Monday is Lane A — a new delivery, skimmed in five minutes. Wednesday is Lane B — the hour, where something gets finished. That split was Barbara's, and it maps onto the lane structure better than a single event would: it gives the *done* gesture a recurring moment of its own, which is exactly what `A-08` doubts will happen on its own.

**Note the two cadences are different things and must not be conflated.** Delivery cadence is weekly (`A-02`, still an assumption under test). Review cadence is twice weekly. A future session must not read "two events per week" as evidence that deliveries are twice weekly.

**How opens are counted for `A-10`'s falsifier:** by delivery cycle, not by event. The falsifier is *three deliveries, fewer than two opened means the channel is wrong.* With two events per delivery cycle, an open on either counts once for that cycle.

---

## Next observation points

- **16–17 Sep** — first expiry. Whatever is unkept clears; record how much, and whether Barbara notices missing anything (`A-01`).
- **14 Sep** — Delivery 003, third cycle. Completes `A-10`'s three-delivery count.
- **First three completions** — `D-15` becomes measurable.
- **Second cycle keep rate** — the discriminator between readings 1 and 2 above.
