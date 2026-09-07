# Current Depth v1.8 Codex Review

**Review target:** `0fc7dfe7e7d3551d6997724763d97e5fd203d3e7`
**Review type:** Independent adversarial product/design review
**Scope boundary:** No implementation plan and no technical architecture design.

## What Matters Now

- The core product direction is coherent, but the current prototype does not yet embody several load-bearing decisions it claims to test.
- The D-11 evaluation is directionally right, but in its current form it cannot reproducibly answer the full claim made for it.
- Several assumptions have hardened into delivery defaults, especially weekly cadence, ten-day expiry, and calendar arrival behavior.
- The project is not ready for a full UI/design pass as a settled product. It is ready only for a narrow prototype usability pass after the evidence gaps below are corrected.

## What I Verified

- The target commit exists.
- At that commit, Git tracks the requested artifacts: `README.md`, `AGENTS.md`, `docs/product-brief.md`, `docs/plans/2026-09-06-product-clarification-plan.md`, `docs/evals/README.md`, `docs/evals/held-out-2026-08-24.md`, and `prototype/current-depth.html`.
- In the current filesystem, `docs/reviews/` exists and this review file did not already exist before writing.

## Findings

### BLOCKING: The prototype sends reading back through Gmail instead of making Lane B the reading surface

The brief says D-22 is Confirmed: Lane A carries pointers only, and a kept item pulls full text onto the Lane B shelf (`docs/product-brief.md:227`). The same section says Gmail is bypassed by pointing at each item's public web version, with full text pulled only when kept (`docs/product-brief.md:320`). The prototype does the opposite: every item is addressed by a Gmail thread id, `gmail()` builds a Gmail URL (`prototype/current-depth.html:625`), the footer says links open the original in Gmail (`prototype/current-depth.html:564`), and keeping an item stores title/source/thread/timestamp only (`prototype/current-depth.html:853`).

Why this matters: the original defect is that reading lives inside an obligation container. Delivery 001 still requires opening that container for the actual reading. It also means keep-to-done latency can record shelf manipulation without proving that Lane B supports deliberate reading.

### BLOCKING: Lane A expiry is asserted but not enacted

D-02 says Lane A items expire on their own (`docs/product-brief.md:207`), Section 3 says they expire after roughly ten days and leave no residue (`docs/product-brief.md:174`), and A-01 is supposed to be tested by observing what expires unkept (`docs/product-brief.md:281`). The prototype only calculates a display string for days left (`prototype/current-depth.html:633`) and leaves the item live unless the user keeps or hides it (`prototype/current-depth.html:638`, `prototype/current-depth.html:725`). When the window reaches zero, the label becomes "clears today"; no item clears.

Why this matters: absence being free is the central behavior, not cosmetic text. If old deliveries stay actionable, the pilot becomes another list and cannot test A-01 or D-02.

### BLOCKING: The D-11 chronological baseline is not reproducible from the held-out set

The eval protocol says the baseline is "the five most recent items at delivery time" (`docs/evals/held-out-2026-08-24.md:27`). The candidate table records dates, not timestamps, and one row spans `28-30 Aug` (`docs/evals/held-out-2026-08-24.md:75`). Multiple candidates share the same dates (`docs/evals/held-out-2026-08-24.md:67`, `docs/evals/held-out-2026-08-24.md:73`).

Why this matters: if two reviewers can compute different chronological top fives, D-11 cannot fairly decide whether a ranking beat reverse chronological. This should be fixed before any ranker output is compared.

### IMPORTANT: Decision status has drifted across artifacts

The brief says v1.8 has twenty-one of twenty-two decisions Confirmed and only D-21 is Proposed (`docs/product-brief.md:5`, `docs/product-brief.md:226`). The plan says every decision is Confirmed, "nineteen of nineteen" (`docs/plans/2026-09-06-product-clarification-plan.md:12`). README agrees with the brief's twenty-one of twenty-two count (`README.md:39`).

Why this matters: D-21 is exactly the kind of detail that can accidentally become architecture. A page reached by a stable link may be the right pilot shape, but the record currently both preserves and erases its Proposed status.

### IMPORTANT: Weekly cadence and ten-day expiry have become defaults before A-02 and A-03 are validated

The brief labels weekly cadence and the derived ten-day expiry as assumptions, not decisions (`docs/product-brief.md:282`, `docs/product-brief.md:283`). The plan then says "Each week Claude produces a delivery" (`docs/plans/2026-09-06-product-clarification-plan.md:28`), and the prototype presents Delivery 001 as a ten-day weekly window (`prototype/current-depth.html:482`, `prototype/current-depth.html:519`).

Why this matters: cadence controls how much attention the system asks for, how expiry feels, and whether the cap of five is starved or bloated. It is fine to test weekly plus ten days, but the artifacts should keep saying "test parameter," not "settled product behavior."

### IMPORTANT: Calendar arrival rests on a new assumption that is not labeled as an assumption

D-20 is Confirmed: Lane A arrives as a recurring calendar event (`docs/product-brief.md:225`). The rationale claims a calendar is opened daily and that past events recede instead of accumulating (`docs/product-brief.md:239`). That may be true, but the reviewed artifacts do not show it was measured. The plan's exit condition says three cycles or Barbara stops opening them (`docs/plans/2026-09-06-product-clarification-plan.md:39`), while the current prototype is still just a page she opens.

Why this matters: "arrives, not fetched" is a core product decision. If the calendar assumption fails, better ranking will not rescue the design. This needs to be treated as an assumption under test, not as a proved property of the medium.

### IMPORTANT: D-11 currently tests ranking inside a prefiltered set, not the full prioritization problem

The held-out set is "field-adjacent only" (`docs/evals/held-out-2026-08-24.md:40`) and excludes non-field streams, while explicitly saying the exclusion rule can be challenged (`docs/evals/held-out-2026-08-24.md:84`). The brief still has open questions about what counts as signal and what a Source is when sender identity fails (`docs/product-brief.md:312`, `docs/product-brief.md:315`).

Why this matters: a ranker can beat chronological order on a human-prefiltered field-adjacent set and still fail the actual job, which includes promotional filtering, source identity, duplicates, and out-of-field-but-subscribed material. The eval should not claim to validate "the prioritization layer" without naming that boundary.

### IMPORTANT: The labelling protocol does not say what evidence Barbara labels from

The prototype says Delivery 001 was picked from subject lines and preview text, not full articles (`prototype/current-depth.html:562`). The held-out table gives source and title only (`docs/evals/held-out-2026-08-24.md:42`). The protocol asks Barbara to mark Y/N for whether each item deserved one of five slots (`docs/evals/held-out-2026-08-24.md:25`), but does not say whether she should label from title, preview, original article, or some fixed excerpt.

Why this matters: labels made from richer evidence than the ranker sees can penalize the ranker for not knowing unavailable facts; labels made from thinner evidence than the delivery selection used can be noisy. Either may be acceptable, but the eval has to state it.

### IMPORTANT: D-19 is described as item-level evidence, but Delivery 001 only discloses aggregate buckets

D-19 says what is never surfaced is recorded alongside what expires unkept (`docs/product-brief.md:224`). The rationale says this lets D-11 be tested against discarded material rather than only against what was shown (`docs/product-brief.md:249`). The prototype discloses dropped material only as aggregate counts and category summaries (`prototype/current-depth.html:544`).

Why this matters: aggregate disclosure is useful for trust, but it is not enough to audit selection or construct a held-out comparison later. If D-19 means item-level evidence, Delivery 001 does not satisfy it. If D-19 only means a qualitative disclosure, the brief overclaims its evaluation value.

### IMPORTANT: The primary success criterion is necessary but too narrow to carry the whole success claim

D-15 defines success as median keep-to-done latency of 14 days or less after at least three done items (`docs/product-brief.md:220`). The eval README describes this as "Does the system produce reading?" (`docs/evals/README.md:19`). The prototype foregrounds that metric (`prototype/current-depth.html:489`). But D-15 only measures items that were kept and marked done; it does not measure whether Lane A was opened, whether surfaced items were worth skimming, whether anything was kept, or whether A-08 holds.

Why this matters: the project can fail the human goal before D-15 ever becomes measurable. Conversely, it can achieve a low keep-to-done latency on a tiny number of unusually easy keeps while not improving current awareness. D-15 should remain preserved, but the artifacts should stop implying it alone proves the system produces reading.

### IMPORTANT: D-10 is confirmed but neither the prototype nor the eval exercises it

D-10 requires that relevance be inspectable and editable: Barbara can see what the system believes she cares about, see why an item surfaced, and change both (`docs/product-brief.md:215`). The prototype includes item-level "why" text, but no editable interest profile. The "less like this" control records a source signal (`prototype/current-depth.html:861`) without exposing the underlying belief it modifies.

Why this matters: inspectability is a product requirement meant to prevent plausible but arbitrary ranking. D-11 tests outcome against chronological order; it does not test whether explanations or profile edits are usable or faithful.

### OPTIONAL: The current design language is quiet and appropriate, but it may underplay the arrival boundary

The prototype has a restrained reading-desk feel and avoids gamified pressure. That fits D-16 and D-17. The weak spot is that "Delivery 001" and the page itself can make the manually opened page feel like the product, while D-09/D-20 say the arrival channel is part of the product.

Why this matters: this is not a reason to redesign the visual system now. It is a reminder that a later UI pass should treat arrival state, expiry state, and Lane B reading state as product behaviors, not just page sections.

## What Is Solid Enough To Preserve

- The Lane A / Lane B split is the strongest product decision. Current awareness and deliberate study really do want different surfaces.
- The caps of five and seven are defensible as pressure against accumulation, provided cadence remains explicitly under test.
- D-16 is an important guardrail: metrics should come from gestures Barbara would make anyway.
- D-11's delete-or-keep stance is healthy. The ranker should have to earn its existence.
- The early hand-made delivery was the right move for the "building replaces reading" risk, as long as the prototype is not mistaken for proof.

## Resolve Before Architecture

- Reconcile D-21's status across the brief, plan, README, and prototype.
- Make expiry real in the pilot or stop claiming the pilot tests expiry.
- Decide whether Lane B must contain extracted reading text now, or explicitly label Delivery 001 as a partial pilot that still falls back to Gmail.
- Define D-19's evidence granularity: item-level discarded candidates or aggregate disclosure.
- Make the D-11 baseline reproducible and specify what evidence Barbara labels from.
- Limit the D-11 claim to the part of prioritization it actually tests, unless source filtering and promotional filtering are included.
- Treat calendar arrival as an assumption under test, with a clear way to record opens or non-opens that does not create a new user gesture.
- Keep A-02 and A-03 visibly provisional until cadence has evidence.
- Decide how D-10 will be validated at the product level, separate from ranker accuracy.

## UI/Design Pass Readiness

Not ready for a full UI/design pass as a settled product. Too many behavior-level contradictions would get prettified into apparent decisions.

Ready for a narrow prototype pass only: improve legibility, interaction clarity, and state visibility around the current pilot while preserving the unresolved labels above.
