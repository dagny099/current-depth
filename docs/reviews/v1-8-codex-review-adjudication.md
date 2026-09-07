# Adjudication — Codex review of brief v1.8

**Adjudicated** 6 Sep 2026, Claude Code (Opus 5)
**Review under adjudication** `docs/reviews/v1-8-codex-review.md`
**Review target** commit `0fc7dfe`
**Verified** `git diff --stat 0fc7dfe HEAD` returned one file — the review itself — so every finding was checked against the artifacts Codex actually saw, not a later state.

---

## What matters now

- **Codex found real defects.** Nothing was rejected outright. Three findings genuinely blocked further evidence-gathering.
- **Its recurring error is category confusion:** it read *Delivery 001 limitations* and *stale plan wording* as *product-decision defects*. Only one finding touched a Confirmed decision, and there the prototype simply predates the decision by a few hours.
- **The drift was worse than reported.** Section 10 of the brief was stale in all four of its numbered items; the plan contradicted itself on question 4. Codex caught neither.
- **A fourth eval defect surfaced during the repair, more serious than the one Codex reported:** the held-out corpus was an incomplete sample of its own window, with no recorded inclusion rule. Barbara set the rule the same day — everything field-adjacent, promotional included — and the corpus was rebuilt from 34 units to 62. It also **reversed the difficulty of D-11**, making the chronological baseline weaker rather than stronger.
- **No new metric or success criterion was created.** Several claims were narrowed to what they actually test; nothing was added to measure.

## Scoreboard

| # | Finding | Verdict |
|---|---|---|
| BLOCKING 1 | Prototype sends reading back through Gmail instead of Lane B | **Partially accept** |
| BLOCKING 2 | Lane A expiry asserted but not enacted | **Accept** |
| BLOCKING 3 | D-11 chronological baseline not reproducible | **Accept, and worse than stated** |
| IMPORTANT 1 | Decision status drifted across artifacts | **Accept** |
| IMPORTANT 2 | Weekly cadence / ten-day expiry hardened into defaults | **Partially accept** |
| IMPORTANT 3 | Calendar arrival rests on an unlabelled assumption | **Partially accept** |
| IMPORTANT 4 | D-11 tests ranking inside a prefiltered set | **Partially accept** |
| IMPORTANT 5 | Labelling protocol does not say what evidence she labels from | **Accept** |
| IMPORTANT 6 | D-19 described as item-level, disclosed as aggregate | **Partially accept** |
| IMPORTANT 7 | D-15 too narrow to carry the whole success claim | **Partially accept (framing only)** |
| IMPORTANT 8 | D-10 confirmed but exercised by neither prototype nor eval | **Partially accept** |
| OPTIONAL | Design language may underplay the arrival boundary | Deferred, agreed |

---

## The findings, one at a time

### BLOCKING 1 — Gmail rather than Lane B as the reading surface → partially accept

**Right on every citation.** `gmail()` in the prototype, the footer note, and `doKeep` storing only title/source/thread/keptAt. D-22 is Confirmed and says the opposite. The contradiction is real.

**Overstated.** Codex framed this as the prototype contradicting a settled decision. The prototype was written before D-22 was ratified the same day. It is a first-delivery limitation, not a design defect, and D-22 needs no revision. Its second clause — that keep-to-done can record shelf manipulation without proving reading — is true but is A-08 restated, which the brief already carries as an open assumption.

**Done:** the D-22 rationale now says plainly that Delivery 001 predates and does not satisfy it, and that Delivery 002 onward carries canonical URLs and embedded text.
**Open:** the change itself lands when Delivery 002 is built. Deliberately not pre-built — a mechanism with no data to exercise it would be speculative.

### BLOCKING 2 — expiry asserted but not enacted → accept

**Right, completely.** `daysLeft()` clamped at zero and `statusOf()` returned `live` forever. At day ten the page said "clears today" and nothing cleared.

This was the one finding where the gap actively produced *false* evidence: a page promising self-clearing that never clears teaches the wrong lesson about the exact mechanism A-01 exists to test, and leaves A-01 with no evidence base at all.

**Done.** `sweepExpired()` stamps untouched items `expired` at the window's end — not at the moment she opens the page, so the record stays truthful about when it cleared. Expired items leave the surface entirely rather than lingering struck-through, because residue would mean she could never notice missing one; a quiet aggregate line replaces them. Verified at three window positions: fresh (nothing expires), day 10 (all five, idempotent on re-sweep so there is no save loop), and day 20 with a pre-kept and pre-hidden item (both survive untouched, only the three untouched expire). No new gesture, so D-16 holds.

### BLOCKING 3 — baseline not reproducible → accept, and worse than stated

**Right** about dates-without-timestamps and ties.

**Two defects Codex missed, and a third it had no way to see:**
- Row 32 collapsed **three** DATAVERSITY items into one row with a single `Y/N` cell — 34 items in 32 rows.
- "The five most recent **at delivery time**" had no t=0; no delivery was ever made for that week.
- The window label "24–31 Aug" was wrong at both ends — nothing on 24 Aug, nothing on 31 Aug — and 31 Aug overlapped Delivery 001's own week, which would have broken the hold-out.

**Done.** Timestamps verified against the mailbox in a second read-only pass; row 32 split into 32a/32b/32c (one of which is 27 Aug, so the old span was wrong too); `t0 = 2026-08-31T00:00:00Z` fixed; tie-break rule added (rows 16 and 32a tie exactly); the duplicate in row 16 recorded as one item per F-05; the baseline precomputed and marked as needing recomputation if the corpus changes.

### New, found during the repair — the corpus is an unexplained sample

Not in Codex's review. The capture omits at least six field-adjacent items from the same window and from sources already in the brief's Section 1.5 — an AINews issue, a Lenny's issue, a Pragmatic Engineer deep dive, a Nate's issue, a Ken Huang piece, a DeepLearning.AI campaign. It also omits Academia.edu entirely (6 items) while including two `hello@deeplearning.ai` items that Section 1.5 classifies as course marketing — and those two are the *same campaign* four minutes apart to two addresses, with different subject lines and an identical preview, so they form a near-duplicate pair that thread-id dedup will not catch.

This outranks the timestamp defect. "The five most recent" over an incomplete corpus is not the chronological baseline; it is the chronological baseline of a sample whose rule was never written down.

**Resolved 6 Sep 2026 by Barbara: everything field-adjacent in the window, promotional items included.** The corpus was rebuilt to that rule and went from 34 labelling units to **62** — squarely inside F-04's independent estimate of 55–70 field-adjacent messages per week, which is the corroboration the 34-item sample never had. The window is now a principled 24–30 Aug rather than whatever happened to be captured. Labelling is unblocked.

**Two consequences worth carrying forward.** First, the decision *reversed the difficulty of D-11*: with promotional mail included, two of reverse-chronological's top five are a webinar promotion and an automated Academia.edu recommendation, so the baseline is **weaker** than the prefiltered sample suggested and easier to beat. An earlier draft of this adjudication argued the opposite, on the prefiltered corpus; that reasoning no longer applies. The threshold has to be set knowing a ranker can clear this bar simply by declining to surface marketing. Second, completing the corpus exposed a duplication pattern that neither thread-id nor subject-line dedup can catch: Maven and DeepLearning.AI each send one campaign to her two addresses under *different subject lines* with identical preview text, while The Batch uses a single thread for both. Two duplication shapes in one mailbox, recorded as evidence for questions 10 and 12 rather than collapsed, since how duplicates are collapsed is still open.

### IMPORTANT 1 — status drift → accept

The plan said "nineteen of nineteen"; there are 22 decisions and D-21 is Proposed.

**Overstated.** Codex said the record "both preserves and erases" D-21's status. It did not — the plan never mentions D-21, it miscounted, and both the brief and `AGENTS.md` make the brief authoritative on firmness. A stale number, not an epistemic breach.

**Done.** Corrected in the plan, with a note naming what it previously said and why the brief governs.

### IMPORTANT 2 — cadence and window hardened → partially accept

**Right** that one plan sentence read declaratively.

**Substantially overstated.** The brief still labels these A-02 and A-03, and the plan's own Phase 1 table lists them as open *with options*. Codex read one line in isolation. A pilot cannot run without picking values, and picking a test parameter is not ratifying it. The prototype's unhedged interface copy is correct copy — an interface is not caveated with "test parameter".

**Done.** One paragraph added to Phase 0 naming weekly and ten days as test parameters. Nothing changed in the brief or the prototype, because nothing there was wrong.

### IMPORTANT 3 — calendar assumption unlabelled → partially accept

**Right** that "a calendar is opened daily and past events recede" is inference about Barbara sitting inside a Confirmed decision's rationale, where it reads as though it had been checked.

**Codex missed the falsifier**, which the brief had already fixed in advance: three deliveries, fewer than two opens means the channel is wrong rather than the content. The assumption was already under test; it lacked only an identifier.

**Done.** Added as **A-10**, pointed at that existing falsifier. On the D-16 worry Codex raised about recording opens: a page load is not a gesture she makes *for* the measurement, so passive counting is already permitted. No new gesture, no new metric.

### IMPORTANT 4 — D-11 tests a prefiltered set → partially accept

**Right** that the claim needed scoping.

**Codex missed the direction of the bias.** Prefiltering makes reverse-chronological a *stronger* opponent, not a weaker one — chronological order over already-relevant material is harder to beat than over raw mail. So this is a labelling problem, not a validity problem, and the bias runs against the ranker, which is the safe direction under a test whose default answer is delete.

**Done.** Scoping paragraphs in the brief's D-11 rationale, `docs/evals/README.md`, and the corpus file. **Deliberately not done:** expanding the corpus past field-adjacent. That is question 11, and hand-labelling the general-inbox remainder would be a different and far costlier evaluation.

### IMPORTANT 5 — labelling evidence unspecified → accept

**Right**, and the reasoning about noise in both directions is sound.

**Done.** Labels are made from source, subject and preview text — matching what the picker saw when it built Delivery 001, so labels and ranker face the same evidence. Preview snippets were captured for all 34 items while the connector was still switched.

**A cost Codex did not surface, now recorded:** preview text is not uniformly informative. HackerNoon's is identical boilerplate across all seven of its items, so those are effectively title-only; Academia.edu and LinkedIn truncate mid-sentence. The handicap is symmetric, but a labeller needs to know that a thin preview is a property of the source rather than a signal about the item.

### IMPORTANT 6 — D-19 granularity → partially accept

**Right** that the ambiguity exists.

**Conflating two obligations.** D-19 says *recorded*; the page's five buckets are *disclosure*. Both can be satisfied at once. Codex's claim that aggregates block "constructing a held-out comparison later" is also wrong — the held-out set was captured independently of any delivery.

**Done, as a question rather than an answer.** Opened as question 15 with a recommendation: item-level record in the repo, aggregate disclosure on the page, record scoped to field-adjacent candidates rather than all ~200. The D-19 rationale now says the decision stands and only its granularity is open. Until Barbara settles it, Delivery 001 should not be described as either satisfying or violating D-19.

### IMPORTANT 7 — D-15 too narrow → partially accept, framing only

**Right** that `docs/evals/README.md` overclaimed by heading D-15 "Does the system produce reading?".

**Overstated.** The brief already carries three secondary diagnostics, already forbids promoting them, and already names A-08 as the validity threat. Codex's own ask was only that the artifacts stop implying D-15 alone proves it.

**Done.** The heading now reads "How long does a kept item take to finish?", with an explicit note on what D-15 is silent about and an explicit refusal to add a companion criterion. This was the finding most likely to grow a metric if handled loosely, and it did not.

### IMPORTANT 8 — D-10 not exercised → partially accept

**Right on the facts.** Per-item "why" exists; an editable interest profile does not, and `doHide` records a source signal without exposing the belief it changes.

**Miscategorised.** D-10 is a requirement on the built system, not on Delivery 001. An editable interest profile is ranker-adjacent and belongs to the deferred phase.

**Open.** How D-10 gets validated at the product level, separately from ranker accuracy, is a decision for the architecture phase. A cheap half is available meanwhile if Barbara wants it: a static paragraph stating what the picker believed she cares about is inspectable without being editable.

---

## What Codex got right that is worth keeping on the record

Its "What Is Solid Enough To Preserve" section is accurate and useful, and its readiness verdict is correct: not ready for a full UI pass as a settled product, ready for a narrow prototype pass. The two behaviour fixes above are what unblock that pass. Its instinct to check the artifacts against each other rather than reading the brief alone is what surfaced the drift, and that is the part of the method worth repeating next cycle.

## Still open after this adjudication

| Item | Owner | Blocks |
|---|---|---|
| ~~The corpus inclusion rule~~ | ~~Barbara~~ | **Closed 6 Sep 2026** — everything field-adjacent, promotional included; corpus rebuilt to 62 units |
| The D-11 threshold blanks | Barbara | D-11 comparison |
| Question 15 — D-19 record vs disclosure granularity | Barbara | nothing yet |
| D-22 in practice — canonical URLs, embedded text | Delivery 002 | nothing yet |
| How D-10 is validated at product level | architecture phase | nothing yet |
| A-02 / A-03 — cadence and window | evidence from delivery cycles | nothing yet |

## Experiment accounting

Per `AGENTS.md` section 5: this cycle changed **both model and harness** at once. It is an operational benchmark of Claude Code + Opus 5 against Codex, and carries no claim about model quality in either direction.
