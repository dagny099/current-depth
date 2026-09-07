# Product clarification plan

**Created** 6 Sep 2026
**Input** `docs/product-brief.md` v1.9 (reviewed at v1.8)
**Status** Revised 6 Sep 2026 after Barbara realigned the session's goal, then corrected 6 Sep 2026 after independent review. Delivery 001 shipped; Phase 0 running. **Reviewed** by Codex against brief v1.8 (`docs/reviews/v1-8-codex-review.md`) and **adjudicated** (`docs/reviews/v1-8-codex-review-adjudication.md`).
**Scope** Get a usable deliverable into her hands, settle the logic and the design behind it, and leave it in a state another session or harness can make pretty. Architecture stays out of scope — no storage design, no pipeline, no vendor selection.

---

## Where the project actually stands

Twenty-one of the ledger's twenty-two decisions are `Confirmed`; **D-21 remains `Proposed`** — whether the delivery is a page reached by link rather than content carried in the message. Barbara said "probably a page" and never ratified it, and D-21 is exactly the kind of detail that could drift into architecture unnoticed, so the count matters. *(Corrected 6 Sep 2026: this line previously read "nineteen of nineteen", which both undercounted the ledger and erased D-21's status. The brief's Section 4 is authoritative for firmness, not this plan.)*

Either way, the point stands: **the decision ledger has stopped being the bottleneck.** What is left is not more deciding. It is evidence.

Five of the eight original unresolved questions are closed. The remaining open items are cheap, with one exception: D-11 is now ratified, which means a hand-labelled evaluation set has to exist before a prioritisation layer does. That is the longest lead-time item in the project and nothing else depends on it, so it should start early and run in parallel.

The sharpest risk in the brief is Section 9's *"building it replaces reading."* Barbara's own instinct — ship something usable immediately, keep the build small — is a better answer to it than a research programme was, which is why this plan was reordered around a working deliverable rather than a study.

**Barbara's stated goal for this session, in her words:** *"I want to get to something I can use as soon as possible, and I want to hammer out the logic and a decent design here, so that in another session or harness, I can make it pretty."* Everything below serves that.

---

## Phase 0 — Weekly delivery, produced for her (running)

> **Rewritten 6 Sep 2026.** The original Phase 0 had Barbara hand-picking the five items herself. That was wrong: it made her do the exact job the system exists to do, and she said so. **Claude picks; she reads.** Same evidence, none of the labour — and a better test, because it exercises the selection as well as the container.
>
> It also dissolves the phase. There is no separate manual pilot: the deliverable *is* the pilot, and the measurement is built into it. `prototype/current-depth.html` records keep and done timestamps, so D-15 accrues from ordinary use.

Claude produces a delivery each week: five items chosen from her subscribed sources under D-18, with the dropped material disclosed under D-19. Barbara reads it, keeps what matters, finishes what she keeps. Nothing else is asked of her.

**Weekly is the test parameter, not a settled product behaviour.** Cadence is A-02 and the ten-day window is A-03, both still assumptions — a pilot cannot run without picking values, but picking them is not ratifying them. If the rhythm turns out wrong, the cap of five stays and the cadence moves.

Why this comes first:

- It is the **only direct mitigation** for the Section 9 risk. Something usable exists now, so the project has delivered reading before any system was built.
- It tests **A-01** (does expiry suit her, or does she keep wishing she still had something), **A-02 / A-03** (is the cadence and window right — living with it answers this better than choosing in the abstract), **A-08** (will she actually mark done), **A-09** (does hiding turn Lane A into a surface she clears) and **D-15** (is a 14-day median keep-to-done realistic).
- It exercises **D-18's cap of 5** against reality. If 5 feels starved or bloated, that is far cheaper to learn now.
- It produces the first real **Completion Record** (D-17), which is the encouragement artifact.

The page records this by itself: surfaced, kept, done, and each "less like this" signal. That is enough for D-15 and for all three diagnostics. D-19's dropped material is disclosed in the delivery rather than hidden.

**Exit condition:** three delivery cycles completed, or Barbara stops opening them — which is itself the most valuable finding this project could produce and must be recorded rather than quietly retried.

**Open for delivery 002 onward:** how the delivery reaches her. Right now it is a page she opens, so D-09's "arrives, not fetched" is **decided but not yet in force** — the mechanism is settled (a recurring calendar event she creates by hand, D-20, closing question 4), and what is missing is that she has not created the event yet. *(Corrected 6 Sep 2026: this paragraph previously called question 4 unresolved, contradicting the Phase 1 table below, which correctly marks it closed.)*

What remains open here is not the mechanism but whether it works: A-10 assumes a calendar is a channel she actually opens. The falsifier is already fixed — three deliveries, fewer than two opens means the channel is wrong rather than the content.

---

## Phase 1 — Close the remaining product questions (one sitting)

All are cheap. None blocks Phase 0. Several will be answered better *after* a week of Phase 0, which is the argument for not front-loading them.

| Question | What has to be decided | Note |
|---|---|---|
| A-02, A-03 | Cadence, and the expiry window that follows from it | Best answered from Phase 0 experience. Options at a fixed cap of 5: 5 weekly, or 3 twice-weekly — same throughput, different rhythm. Barbara's rejection of a month-long evaluation window suggests a preference for the faster one |
| ~~4~~ | ~~How Lane A arrives~~ | **Closed** — a recurring calendar event she creates by hand (D-20). All three original candidates were broken |
| 7 | The gesture name | The brief writes **keep** throughout for consistency; this needs a nod, not a debate |
| 8 | How far related content extends beyond TED talks | Papers? Conference talks? Confined to Lane B by D-06 either way |
| 10 | Which of the six delivery addresses are in scope, and how duplicates are collapsed | F-05. The same issue arrives twice today |
| 11 | What counts as signal | Narrower than it was. The fields and the subscriptions now agree; what remains is the non-field stream sharing the same labels, and the promotional share of the vendor sources. DeepLearning.AI is a usable quality anchor — Barbara named it |
| 12 | What a Source is when the sender address is not the publication | Four LinkedIn publications share one sender address. Sender-based identity fails |
| 13 | Where the page lives — Artifact or her own infrastructure | Self-hosting a static page is easy; re-solving synced state is not. Choosing a host is tool selection, so it belongs to the architecture phase |
| ~~14~~ | ~~Does the delivery carry the reading or point at it~~ | **Closed** — pointers in Lane A, full text pulled on keep (D-22) |

---

## Phase 2 — Build the D-11 evaluation set (critical path, start early)

D-11 is ratified, and it is exacting: any prioritisation layer must beat a chronological baseline on a hand-labelled set, against a threshold **written down in advance**, or be removed. That obligation binds now, not later, because the set has to exist before the thing it judges.

Steps:

1. ~~Capture a corpus.~~ **Done 6 Sep 2026, completed the same day** — `docs/evals/held-out-2026-08-24.md`, now **62 labelling units** from 24–30 Aug, a week Delivery 001 was deliberately *not* built from. The first capture held 34 and was found to be an unexplained sample of its own window; Barbara then set the inclusion rule — everything field-adjacent in the window, promotional and automated mail included — and it was rebuilt to that rule. 62 units sits inside F-04's independent 55–70 per week estimate.
2. **Label it by hand.** For each item: would this have been worth surfacing? Barbara labels; nobody else can.
3. **Define the chronological baseline.** The most recent 5 items at delivery time — the thing to beat. **Not trivial to compute, as first assumed.** The review found the captured table carried dates rather than timestamps, no anchor for "delivery time", ties on almost every date, and one row bundling three DATAVERSITY items together. Two labellers could compute different top fives, which would void the comparison. Repaired in the corpus file; re-verify before comparing anything.
4. **Write the threshold down before looking at any ranker output.** For example: the ranked 5 must contain at least N of the labelled keep-worthy items, versus the baseline's M. The number is Barbara's call; the discipline of fixing it in advance is D-11's whole point.
5. **Record results in `docs/evals/`.** The corpus and protocol are already there; the labels and the comparison go alongside them.

This is a delete-or-keep test, **not** a training loop. Nothing learns from these labels. If a ranker cannot beat reverse-chronological, D-11 says remove the ranker.

Removing the prioritisation layer counts as a good outcome. The eval is not there to justify building a ranker; it is there to find out whether one is warranted.

---

## Phase 3 — Cross-harness review (the experiment the README sets up)

**First cycle complete, 6 Sep 2026.** Codex reviewed brief v1.8 from commit `0fc7dfe` on the remote; the review is in `docs/reviews/v1-8-codex-review.md` and the adjudication alongside it. Steps 1–5 below all ran. Step 6's accounting: **both model and harness changed at once**, so this is an operational benchmark and carries no claim about model quality.

The sequence, retained because it repeats each cycle, per `README.md` and `AGENTS.md` section 5:

1. Freeze the brief at its then-current version as the shared input.
2. This plan, revised by what Phases 0–2 found, becomes the durable artifact.
3. **Codex reviews it independently** — receiving the artifact and the brief, *not* this conversation or any Claude Code reasoning history. That independence is the experiment.
4. The review lands in `docs/reviews/`.
5. Claude Code adjudicates the findings; the revised plan supersedes this one.
6. Record which variables changed. A Claude Code / Codex comparison changes both model and harness at once, so it is an operational benchmark and not a model-quality result. Say so.

**Frozen input — now available.** The remote is up at `github.com/dagny099/current-depth`. Freeze by tag or commit SHA and hand Codex *that reference*, not a copy pasted into a prompt: a pasted copy cannot be verified as identical afterwards, which would quietly undo the independence the whole experiment rests on.

---

## Phase 4 — Architecture

**Authorised 7 Sep 2026.** The restriction is retired; see Section 0 of the brief and `AGENTS.md` section 3.

The phrasing this section used to carry — "every one of them is better decided after Phases 0–2 return evidence" — is exactly the sequencing Barbara rejected. Storage, delivery mechanism, ranker implementation and source ingestion get designed when they are needed to make something work, at the smallest scale that works, and revised from use.

---

## Note on this plan, 7 Sep 2026

**Superseded in structure, kept for the record.** Its phases imply a sequence — pilot, then questions, then eval, then review, then architecture — and that sequence is what stalled the project. The current order of work lives in Section 10 of the brief; the operating cycle lives in `AGENTS.md` section 3.

Still worth reading here: the Phase 0 reasoning about why a working delivery came first, the Phase 2 detail on how the D-11 comparison is actually run, and "What would make this plan wrong" below.

---

## Open dependencies and housekeeping

- **Git remote** — configured 6 Sep 2026, `github.com/dagny099/current-depth`. Phase 3 unblocked.
- **Gmail connector** — currently switched to `dagny099@gmail.com`. Capture the Phase 2 corpus before reverting, or accept switching twice.
- **`docs/evals/README.md`** — written 6 Sep 2026. Keeps the two evaluations apart: D-11 (does the ranker deserve to exist) and D-15 (does the system produce reading).
- **A-04, A-06** — carried, not blocking. A-04 is high confidence. A-06 is weakened by F-07 and probably not worth testing.
- **Question 6** — whether expiry survives contact with her habits. Answerable only by Phase 0.

---

## What would make this plan wrong

Recorded so a reviewer has something to aim at:

- If Phase 0 shows Barbara reads nothing even from a hand-curated 5, the problem is not selection or location, and most of this design is treating the wrong cause.
- If the keep rate is far below 20%, a cap of 5 is too small and D-18's arithmetic needs redoing.
- If the hand-labelled set shows chronological order already performs well, D-11 says the prioritisation layer should be removed — and F-07 hints this is possible, since her mail is already filtered and still unread.
- If A-08 fails and she does not mark done, D-15 is unmeasurable and the success criterion has to be rebuilt on something else.
