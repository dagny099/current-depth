# Product clarification plan

**Created** 6 Sep 2026
**Input** `docs/product-brief.md` v1.5
**Status** Proposed. Not reviewed. Not adjudicated.
**Scope** Product clarification and evidence gathering only. This plan does not design architecture and must not be read as authorising it.

---

## Where the project actually stands

Every decision in the ledger is now `Confirmed` — nineteen of nineteen. That is unusual and worth naming plainly: **the decision ledger has stopped being the bottleneck.** What is left is not more deciding. It is evidence.

Five of the eight original unresolved questions are closed. The remaining open items are cheap, with one exception: D-11 is now ratified, which means a hand-labelled evaluation set has to exist before a prioritisation layer does. That is the longest lead-time item in the project and nothing else depends on it, so it should start early and run in parallel.

The sharpest risk in the brief is unchanged and unaddressed: Section 9's *"building it replaces reading."* Every step below is ordered to attack that risk first.

---

## Phase 0 — Manual pilot (start now, runs 3 weeks)

**Do this before anything else, and do not wait for the other phases.**

Barbara hand-picks 5 items each delivery from her existing mail, writes them into a plain text file or note, and lives with the design as specified: keep promotes to a second list capped at 7; "less like this" removes and is noted; nothing is marked read; items not kept are struck out after the expiry window.

Why this comes first:

- It is the **only direct mitigation** for the Section 9 risk. A working paper version means the project has already delivered reading before a line of code exists.
- It tests **A-01** (does expiry suit her, or does she keep wishing she still had something), **A-02 / A-03** (is the cadence and window right — living with it answers this better than choosing in the abstract), **A-08** (will she actually mark done), **A-09** (does hiding turn Lane A into a surface she clears) and **D-15** (is a 14-day median keep-to-done realistic).
- It exercises **D-18's cap of 5** against reality. If 5 feels starved or bloated, that is far cheaper to learn now.
- It produces the first real **Completion Record** (D-17), which is the encouragement artifact.

What to record, minimally: for each item, when it was surfaced, whether it was kept, when it was marked done. That is enough for D-15 and the diagnostics. What was dropped unseen matters too (D-19) but Phase 2 handles that properly.

**Exit condition:** three delivery cycles completed, or Barbara abandons it — which is itself the most valuable finding this project could produce and must be recorded rather than quietly retried.

---

## Phase 1 — Close the remaining product questions (one sitting)

All are cheap. None blocks Phase 0. Several will be answered better *after* a week of Phase 0, which is the argument for not front-loading them.

| Question | What has to be decided | Note |
|---|---|---|
| A-02, A-03 | Cadence, and the expiry window that follows from it | Best answered from Phase 0 experience. Options at a fixed cap of 5: 5 weekly, or 3 twice-weekly — same throughput, different rhythm. Barbara's rejection of a month-long evaluation window suggests a preference for the faster one |
| 4 | How Lane A arrives — message to self, bookmarked destination, or message linking to a destination | D-09 says it arrives rather than being fetched; the mechanism was never settled. The argument for a message is that it borrows a habit she already has |
| 7 | The gesture name | The brief writes **keep** throughout for consistency; this needs a nod, not a debate |
| 8 | How far related content extends beyond TED talks | Papers? Conference talks? Confined to Lane B by D-06 either way |
| 10 | Which of the six delivery addresses are in scope, and how duplicates are collapsed | F-05. The same issue arrives twice today |
| 11 | What counts as signal | Narrower than it was. The fields and the subscriptions now agree; what remains is the non-field stream sharing the same labels, and the promotional share of the vendor sources. DeepLearning.AI is a usable quality anchor — Barbara named it |
| 12 | What a Source is when the sender address is not the publication | Four LinkedIn publications share one sender address. Sender-based identity fails |

---

## Phase 2 — Build the D-11 evaluation set (critical path, start early)

D-11 is ratified, and it is exacting: any prioritisation layer must beat a chronological baseline on a hand-labelled set, against a threshold **written down in advance**, or be removed. That obligation binds now, not later, because the set has to exist before the thing it judges.

Steps:

1. **Capture a corpus while the connector is still switched.** One to two weeks of real arrivals from the `B@B` label, the DATAVERSITY senders, and the field-adjacent `SubStack` senders. This is time-sensitive only in the sense that reverting the connector means switching back to do it.
2. **Label it by hand.** For each item: would this have been worth surfacing? Barbara labels; nobody else can.
3. **Define the chronological baseline.** The most recent 5 items at delivery time. Trivial to compute, and it is the thing to beat.
4. **Write the threshold down before looking at any ranker output.** For example: the ranked 5 must contain at least N of the labelled keep-worthy items, versus the baseline's M. The number is Barbara's call; the discipline of fixing it in advance is D-11's whole point.
5. **Record it in `docs/evals/`.** That directory holds one empty tracked `README.md` today. This is what fills it.

Removing the prioritisation layer counts as a good outcome. The eval is not there to justify building a ranker; it is there to find out whether one is warranted.

---

## Phase 3 — Cross-harness review (the experiment the README sets up)

Only meaningful once Phases 0–2 have produced something worth reviewing. Sequence, per `README.md` and `AGENTS.md` section 5:

1. Freeze the brief at its then-current version as the shared input.
2. This plan, revised by what Phases 0–2 found, becomes the durable artifact.
3. **Codex reviews it independently** — receiving the artifact and the brief, *not* this conversation or any Claude Code reasoning history. That independence is the experiment.
4. The review lands in `docs/reviews/`.
5. Claude Code adjudicates the findings; the revised plan supersedes this one.
6. Record which variables changed. A Claude Code / Codex comparison changes both model and harness at once, so it is an operational benchmark and not a model-quality result. Say so.

**Dependency:** this needs a git remote. Without one, no other machine or harness can obtain the frozen input, and the independence claim is unverifiable.

---

## Phase 4 — Architecture

**Not authorised.** `CLAUDE.md` and Section 0 of the brief both forbid it until Barbara explicitly moves the project into that phase.

Listed here only so the boundary is visible: storage, delivery mechanism, ranker implementation, and source ingestion are all Phase 4 concerns, and every one of them is better decided after Phases 0–2 return evidence.

---

## Open dependencies and housekeeping

- **Git remote** — not yet configured. Blocks Phase 3 entirely.
- **Gmail connector** — currently switched to `dagny099@gmail.com`. Capture the Phase 2 corpus before reverting, or accept switching twice.
- **`docs/evals/README.md`** — tracked and empty. Phase 2 fills it.
- **A-04, A-06** — carried, not blocking. A-04 is high confidence. A-06 is weakened by F-07 and probably not worth testing.
- **Question 6** — whether expiry survives contact with her habits. Answerable only by Phase 0.

---

## What would make this plan wrong

Recorded so a reviewer has something to aim at:

- If Phase 0 shows Barbara reads nothing even from a hand-curated 5, the problem is not selection or location, and most of this design is treating the wrong cause.
- If the keep rate is far below 20%, a cap of 5 is too small and D-18's arithmetic needs redoing.
- If the hand-labelled set shows chronological order already performs well, D-11 says the prioritisation layer should be removed — and F-07 hints this is possible, since her mail is already filtered and still unread.
- If A-08 fails and she does not mark done, D-15 is unmeasurable and the success criterion has to be rebuilt on something else.
