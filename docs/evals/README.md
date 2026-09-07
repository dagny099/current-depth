# Evaluations

Evaluation definitions and results. Two different things get evaluated here, and conflating them is the mistake this directory exists to prevent.

## What lives here

| File | What it is |
|---|---|
| `pilot-log.md` | Running observations from real use — one entry per delivery, plus a standing tally. Where `A-01`, `A-02`, `A-08`, `A-09`, `A-10` and the `D-15` clock accrue evidence. |
| `held-out-2026-08-24.md` | The hand-labelled set D-11 requires. 62 labelling units from 24–30 Aug 2026 — everything field-adjacent in the window, promotional and automated mail included. Unlabelled; threshold not yet fixed. |

## The two evaluations, kept apart

**1. Does the prioritisation layer deserve to exist?** — `D-11`

A delete-or-keep test, run once. Any ranking must beat plain reverse-chronological on a hand-labelled set, against a threshold **written down before the comparison**, or the ranking is removed. Removing it counts as a good outcome.

**This is not training.** Nothing learns from these labels. A learning system would use them to improve; this uses them to decide whether the thing should be built at all.

**What it tests, and what it does not.** The held-out set covers everything field-adjacent in its window, promotional and automated mail included (inclusion rule set 6 Sep 2026). So this test asks whether a ranking beats reverse-chronological *at ordering field-adjacent candidates, promotional filtering included*. It does not test where the field boundary belongs (question 11), how a Source is identified when the sender is not the publication (question 12), or which delivery addresses count (question 10). Do not report a win here as validating "the prioritisation layer" whole.

**Set the threshold knowing the baseline is weak.** Including promotional mail puts a webinar promotion and an automated paper recommendation into reverse-chronological's top five. That is a low bar, and a ranker clears it by declining to surface marketing — without showing any judgment about relevance. A threshold that only requires beating this baseline would certify a ranker that has not earned its place.

**2. How long does a kept item take to finish?** — `D-15`

Median time from keep to done on Lane B, target 14 days or less, judged once at least three items are done. Accrues from ordinary use of the delivery — no separate instrumentation, because `D-16` forbids any gesture that exists only to feed a measurement.

**This heading used to read "Does the system produce reading?", which overclaimed.** D-15 measures the interval between keep and done and nothing else. It is silent on whether Lane A was opened, whether the five were worth skimming, and whether anything was kept at all — and it can look healthy on two or three unusually easy keeps. It stays the success criterion, because a latency measure degrades in the correct direction where a count does not (see the D-15 rationale in the brief). **No companion criterion is being added.** The diagnostics below already cover the gap and must stay diagnostics; inventing a second success metric because a gap can be described is exactly what `D-16` and the brief's Section 4 warn against.

Secondary diagnostics, explicitly **not** success criteria: keep-to-done conversion (evidence for the `D-08` cap), the expiry and never-surfaced record (`D-19`, testing `A-01`), and the hide-to-keep ratio (the tripwire for `A-09`).

## Rules that bind anything added here

- **Whoever picks cannot grade.** Claude selects each delivery, so Claude's picks are never the evaluation set. Label a week no delivery was built from.
- **Thresholds are fixed in advance.** A threshold chosen after seeing results is not a threshold.
- **A negative result is a result.** Record it. `D-11` was written precisely so that "delete this" stays an available answer.
