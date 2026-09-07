# Evaluations

Evaluation definitions and results. Two different things get evaluated here, and conflating them is the mistake this directory exists to prevent.

## What lives here

| File | What it is |
|---|---|
| `held-out-2026-08-24.md` | The hand-labelled set D-11 requires. 32 field-adjacent candidates from 24–31 Aug 2026, unlabelled. |

## The two evaluations, kept apart

**1. Does the prioritisation layer deserve to exist?** — `D-11`

A delete-or-keep test, run once. Any ranking must beat plain reverse-chronological on a hand-labelled set, against a threshold **written down before the comparison**, or the ranking is removed. Removing it counts as a good outcome.

**This is not training.** Nothing learns from these labels. A learning system would use them to improve; this uses them to decide whether the thing should be built at all.

**2. Does the system produce reading?** — `D-15`

Median time from keep to done on Lane B, target 14 days or less, judged once at least three items are done. Accrues from ordinary use of the delivery — no separate instrumentation, because `D-16` forbids any gesture that exists only to feed a measurement.

Secondary diagnostics, explicitly **not** success criteria: keep-to-done conversion (evidence for the `D-08` cap), the expiry and never-surfaced record (`D-19`, testing `A-01`), and the hide-to-keep ratio (the tripwire for `A-09`).

## Rules that bind anything added here

- **Whoever picks cannot grade.** Claude selects each delivery, so Claude's picks are never the evaluation set. Label a week no delivery was built from.
- **Thresholds are fixed in advance.** A threshold chosen after seeing results is not a threshold.
- **A negative result is a result.** Record it. `D-11` was written precisely so that "delete this" stays an available answer.
