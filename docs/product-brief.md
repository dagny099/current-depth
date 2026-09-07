# Reading Digest — Product Brief

**Version** 1.10 · 7 Sep 2026
**Owner** Barbara (single user; this is a personal system, not a product)
**Status** In use. Two deliveries are running at `prototype/current-depth.html`, arriving through a recurring calendar event. Twenty-one of twenty-two decisions are Confirmed; only D-21 is Proposed. Architecture was authorised 7 Sep 2026 and the working model is now design → build → test → iterate (`AGENTS.md` section 3). What remains is evidence, a handful of cheap questions, and the D-11 evaluation — none of which gate the work.

**v1.10 records the first real evidence.** Delivery 002 shipped 7 Sep under D-22, the calendar event exists, and the pilot has produced its first numbers — including a keep rate around 70% against D-18's assumed 20–40%, and a shelf that filled on day one. Observations live in `docs/evals/pilot-log.md`, not here: this document holds decisions and assumptions, and the log holds what use is revealing about them.

**v1.9 was the post-review revision.** v1.8 was reviewed independently by Codex (`docs/reviews/v1-8-codex-review.md`) and adjudicated (`docs/reviews/v1-8-codex-review-adjudication.md`). No decision changed status as a result. What changed: A-10 was added, question 15 was opened, three claims were scoped to what they actually test, and Section 10 was rewritten because every item in it had gone stale.

---

## 0. How to read this brief

You have no access to the conversation that produced this. This brief is intended to be self-contained for the next product-clarification work.

Two conventions matter:

**Every decision below is tagged with its firmness.** `Confirmed` means Barbara explicitly chose it. `Proposed` means it was put to her, went uncontested, and is written into the requirements, but she never affirmatively ratified it. Treat `Proposed` items as revisable on contact with her; do not treat them as settled just because they appear here.

**Assumptions are separated from decisions on purpose.** Several load-bearing parts of this design rest on inference rather than on Barbara's stated behavior. Those are listed in Section 6 with their basis. If you find yourself building something that depends on an assumption, surface it rather than hardening it.

**Status labels control.** Narrative prose, experience sketches, tables, and candidate entities may describe the current working design, but they do not upgrade firmness. When there is any tension, the decision ledger in Section 4 and the assumptions in Section 6 are authoritative for status.

### Out of scope for the next work

> **Superseded in part, 6 Sep 2026.** Barbara has explicitly moved the project out of pure product clarification. Her words: *"I want to get to something I can use as soon as possible, and I want to hammer out the logic and a decent design here, so that in another session or harness, I can make it pretty."*
>
> **Building a working deliverable is now in scope.** The first one exists: `prototype/current-depth.html` — Delivery 001, five real items, the keep gesture, the seven-slot shelf and the D-15 clock. It is a hand-made artifact, not an architecture: no storage design, pipeline or vendor has been chosen or implied by it.
>
> Two restrictions still bind: **no architecture**, which remains a separate and unauthorised phase, and **no inventing answers** to unresolved questions.

> **Superseded again, 7 Sep 2026 — the working model changed.** Barbara: *"We need to change the mindset to Design as soon as Requirements are Understood and Approved by me, then Build and Test and Fail Fast and Iterate."* She named the cause: agents on this project have repeatedly produced plans gated on collecting clean evidence first, and that sequencing stalled the work.
>
> **The architecture restriction is lifted.** Design and build once a requirement is agreed. The operating cycle now lives in `AGENTS.md` section 3 and governs.
>
> **What still binds:** do not invent answers to unresolved questions, and do not build more than was asked for. `D-11` and `D-15` still decide what survives; they no longer gate when work may start.

Originally requested by Barbara, retained for the record:

- ~~Do not design the technical architecture.~~ **Retired 7 Sep 2026.** No storage design, pipeline topology, or vendor was ever chosen under it. What it actually prevented was shipping.
- ~~Do not implement anything.~~ **Retired 6 Sep 2026.**
- **Propose freely; decide nothing.** Surfacing a new product idea is welcome — label it a proposal and put it to Barbara. What is forbidden is moving a question from unresolved to resolved without her saying so, or writing an invented answer into the brief as though it were decided. *(Reworded in v1.8. The earlier phrasing, "do not fill gaps with new product ideas", was read too literally in session and suppressed a good proposal. The rule protects the record, not the silence.)* **Still binding.**

Earlier working documents exist outside this repository, but they are **not required** for this handoff. Do not treat their absence as missing project state. This brief contains the product information needed for the next work; if an external document is later added to the repo, treat it as supplemental unless explicitly designated authoritative.

---

## 1. The problem

Barbara wants to stay current in **data science**, **machine learning**, and **enterprise data management**. She does not. She named two causes: limited time, and an inbox so cluttered that she never clicks a newsletter at all.

Investigation produced three mechanisms. The first two are the design drivers.

### 1.1 The reading lives inside an obligation container

*Interpretation, not measured.*

Newsletters arrive in an inbox. An inbox is where things that might require action live. Opening it means seeing everything unhandled. Reading is optional; obligations are not. So the price of reading includes the price of confronting a backlog, and that price is paid on every attempt. Declining to open the container is the rational response.

The consequence for design: the newsletters are fine. Their **location** is the defect.

### 1.2 Two different goals share one surface

*Confirmed by Barbara.*

Staying current is broad, perishable, low-commitment. Learning something is narrow, durable, high-commitment. These want opposite properties. A single surface serving both serves neither, and the usual failure is that perishable content crowds out durable content because there is always more of it.

### 1.3 Anything that accumulates becomes the original problem

*From prior art; moderate confidence.*

A queue that grows converts a pleasure into a debt. Roughly twenty years of read-it-later tools document this as the dominant end state: saving costs nothing, reading costs effort, the list outgrows the reader, and the reader eventually clears it in one guilty motion and quits.

Confidence note: sources agree on direction, but no save-to-read ratio statistics were found published. Direction reliable, magnitude unmeasured.

### 1.4 What was actually measured

Two mailboxes have now been inventoried: `barbs@geocue.me` (5 Sep 2026) and the real one, `dagny099@gmail.com` (6 Sep 2026). Findings, scoped honestly:

| ID | Finding | Status |
|---|---|---|
| F-01 | That account carries essentially no DS/ML editorial newsletters. Fourteen named publications searched across inbox, archive, spam and trash; one hit, a false positive. | **True but superseded.** It was the wrong mailbox. |
| F-02 | 933 unread of 1,054 (88%). Zero user labels, zero filters. ~6.7 messages/day. One commercial sender alone sent 18 messages in 30 days, exceeding every field-adjacent sender combined. | **Holds.** Corroborates the described deterrent effect. Does not establish causation. |
| F-03 | Unread accumulation is the documented dominant failure mode of read-it-later tools. | **Holds**, moderate confidence (see 1.3). |
| F-04 | Arrival rate and composition at `dagny099@gmail.com`. **Resolved 6 Sep 2026** by a read-only discovery pass. Field-adjacent editorial arrives at roughly **55–70 messages per week**, carrying an estimated **180–280 candidate items per week**. *(Revised upward in v1.4 after the F-06 retraction added the LinkedIn, DATAVERSITY, ODSC and Knowledge Graph Conference streams.)* Total mailbox arrival is far higher: 192,111 inbox messages, 174,073 unread (90.6%), and a one-day sample implies well over 100 threads per day. | **Closed.** Volume is high. |
| F-05 | The mailbox serves at least **six** addresses — `dagny099@gmail.com`, `barbs@balex.com`, `hidalgod@gmail.com`, `bhs@csail.mit.edu`, `bhs@alum.mit.edu`, `inet@balex.com` — and some publications deliver to two of them. Observed: the same `thebatch@deeplearning.ai` issue arriving twice, once per address. | **Holds**, corrected upward in v1.4. Creates a deduplication requirement. |
| F-06 | ~~No enterprise data management sources were found.~~ **Wrong. Corrected in v1.4.** Enterprise data management is well represented — DATAVERSITY (governance, architecture, CDMP, DGIQ/AIGov), ODSC, the Knowledge Graph Conference newsletter, and a LinkedIn newsletter stream on metadata, taxonomy, ontology and semantics. The v1.3 pass missed them because it searched `category:updates` and the `SubStack` / `DL.ai` labels, and this content arrives at `barbs@balex.com` and `bhs@csail.mit.edu` under the `B@B` label instead. | **Retracted and replaced by F-08.** |
| F-07 | This mailbox is heavily organised — roughly 40 user labels, with working filters (`SubStack` 4,390 messages, `DL.ai` 667, `B@B` 23,532). It is the opposite of the unorganised mailbox measured in F-02, yet the unread rate is worse: the `SubStack` label alone is 4,317 unread of 4,390 (98.3%). | **Holds.** Filing happens; reading does not. |
| F-08 | The professional stream is already separated by an existing filter. The `B@B` label (23,532 messages, 15,493 unread) carries the LinkedIn newsletters, ODSC, and much of the field-adjacent mail addressed to `barbs@balex.com`. Enterprise data management arrives mainly through DATAVERSITY at `dagny099@gmail.com`. | **Holds.** A source list can be seeded from `B@B` plus the DATAVERSITY senders. |

F-04 is closed, and it closed in the direction that keeps the design honest: there is more than enough arriving to justify a prioritisation layer, so A-07 holds and D-10 / D-11 become live rather than hypothetical.

F-07 is the more uncomfortable finding. The original story was that clutter deters reading. This mailbox is not uncluttered, but it *is* curated — the newsletters are already filtered into their own labels, away from the inbox — and they still go unread at 98%. Sorting the reading out of the obligation container has, in effect, already been tried here. That does not refute the premise in 1.1, but it does mean relocation alone is not sufficient, and any plan resting on relocation as the primary mechanism should say why this system differs.

### 1.5 Observed sources (discovery pass, 6 Sep 2026)

The D-04 deliverable. This is what she is actually subscribed to, not a proposed source list. Inclusion here is an observation, not a decision.

**Field-adjacent, editorial:**

| Source | Sender | Rough cadence |
|---|---|---|
| AINews / Latent Space | `swyx+ainews@substack.com`, `swyx@substack.com` | Near-daily digest plus essays |
| The Batch | `thebatch@deeplearning.ai` | Weekly |
| Data Points | `datapoints@deeplearning.ai` | 2–3 per week |
| Understanding AI | `understandingai@substack.com` | 3–4 per week |
| Ken Huang | `kenhuangus@substack.com` | Near-daily |
| Nate's Newsletter | `natesnewsletter@substack.com` | 3–4 per week |
| The Pragmatic Engineer | `pragmaticengineer@substack.com`, `+the-pulse` | 2 per week |
| Lenny's Newsletter | `lenny@substack.com` | 2–3 per week |
| Claude Code for Non-Coders | `claudecodefornoncoders@substack.com` | 2 per week |
| Decision | `decision@substack.com` | Weekly |
| Marily Nika / AI PM Academy | `marily@substack.com`, `marily-nika@courses.maven.com` | Weekly, part course marketing |
| HackerNoon | `accounts@hackernoon.com` | Near-daily |
| Academia.edu | `updates@academia-mail.com` | Near-daily |
| Maven | `maven@list.maven.com` | Intermittent, course marketing |
| **Juan Sequeda** (data.world) | `juansequeda@substack.com` | ~2 per week | **Added v1.6.** Knowledge graphs, ontologies, data products, data governance. Delivers to `barbs@balex.com` under `B@B`. The most on-field enterprise-data-management source found so far |
| **Beyond Euclid** | `beyondeuclid@substack.com` | Weekly | **Added v1.6.** Mathematics and science curation |

**Added in v1.4, after the F-06 retraction.** These arrive at `barbs@balex.com` or `bhs@csail.mit.edu`, mostly under the `B@B` label, which is why the first pass missed them:

| Source | Sender | Rough cadence | Note |
|---|---|---|---|
| LinkedIn newsletter — metadata, taxonomy, ontology, semantics (Jessica Talisman) | `newsletters-noreply@linkedin.com` | ~Weekly | Directly on the knowledge-organisation material named in A-04. Recent subjects: "Ontologies and Other Myths", "The Intentional Arrangement SKOS Editor", "The EU AI Act and Descriptive Access", "Thesaurus" |
| The AI Agent Report | `newsletters-noreply@linkedin.com` | Weekly | |
| The AI Table Review | `newsletters-noreply@linkedin.com` | ~Weekly | |
| MIT CSAIL | `newsletters-noreply@linkedin.com` | ~Monthly | |
| LinkedIn News editorial | `newsletters-noreply@linkedin.com` | ~Weekly | Market/careers, not field |
| ODSC | `info@odsc.com` | ~2 per week | One genuine weekly article roundup; the rest conference marketing |
| DATAVERSITY | `info@`, `training@`, `events@dataversity.net` | ~5 per week | Governance, architecture, CDMP, DGIQ/AIGov. Mostly promotion; see A-05 |
| Knowledge Graph Conference | `deb@knowledgegraph.tech` | ~Monthly | Delivered to `bhs@csail.mit.edu` |

All LinkedIn newsletters share one sender address, so a Source cannot be identified by sender alone — the publication name lives in the message, not the envelope. That is a real complication for any source model.

**Vendor / course marketing rather than editorial:** `hello@deeplearning.ai`, `maven@list.maven.com` and the Maven course senders; the bulk of DATAVERSITY; the conference-promotion share of ODSC. Low signal by the standard D-12 sets.

**Sharing the same labels but outside the named fields:** `ryanmcbeth` (military analysis, the single highest-volume sender observed), `whattocook` and `elliekrieger` (cooking), `stephentotilo` (games), `yourlocalepidemiologist` (public health), `georgesaunders` (fiction). These are not noise in the D-12 sense — they appear to be things she chose — but they are not the stated fields either. Question 11.

**Previously reported absent, wrongly:** enterprise data management. See the F-06 retraction and F-08.

---

## 2. The experience we're aiming for

**Working experience sketch — not a decision ledger.** As of v1.10 nearly everything described here is Confirmed. The exception is D-21, still `Proposed`: whether the delivery is a page reached by link rather than content carried in the message. Several behaviours remain assumption-dependent — A-01, A-02, A-08, A-09. Section 4 and Section 6 remain authoritative for status.

Written from Barbara's side of the screen.

Once a week, something arrives carrying a handful of things worth knowing about in her fields. She reads it or she does not. If she does not, nothing happens: no counter climbs, no badge appears, nothing waits for her. The items age out on their own within days and leave no residue. Ignoring it for three weeks costs nothing and leaves the system in a good state.

When something in that weekly arrival is worth more than a skim, she makes **one gesture**. That is the only action available. The item moves onto a small shelf that does not expire and does not grow past its cap. The shelf is where she goes when she has an hour rather than five minutes, and it is the only place the system ever offers her additional material — a related talk, a related paper — because offering more things to read in the weekly stream would be the disease, not the treatment.

The shelf being capped is the mechanism, not a limitation. Adding a new item when it is full requires removing one, which forces a choice she would otherwise defer indefinitely.

Nothing in this experience involves archiving, marking read, or clearing a list. Those actions are absent by design. She can tell the system "less like this," which teaches it and takes the item off the surface, but that is a judgment about the content rather than housekeeping. Disappearance remains the default state, and attention is the only thing that overrides it.

---

## 3. Lane A and Lane B

**Working model.** As of v1.10 the lane structure, both caps, both Lane A actions and the arrival mechanism are Confirmed. This section keeps the design in one place; where a detail is assumed or unresolved elsewhere, that status still governs.

### 3.1 The table

Reproduced from the working session, unchanged in meaning:

| | Lane A — Current | Lane B — Study |
|---|---|---|
| Cadence | Weekly batch | Added by hand, no schedule |
| Lifetime | Items expire ~10 days, silently | No expiry |
| Size | Hard cap: 5 per delivery (D-18) | Hard cap: 7 (D-08) |
| Actions | Keep, less like this | Notes, done |
| Keep does | Promotes into Lane B | n/a |

Terminology note: "favorite" and "keep" refer to the same gesture. This brief now writes it as **keep** throughout for consistency, but the name is still unresolved (question 7) and using it here does not settle it.

The Actions row changed in v1.2. Lane A previously had one action; it now has two, per D-14.

### 3.2 Lane A — Current awareness

Current working behavior:

- Arrives on a weekly cadence. Barbara does not fetch it. A destination she must remember to visit is a destination she will stop visiting. The arrival mechanism is a recurring calendar event she creates by hand, carrying a stable link (D-20).
- Items expire approximately ten days after arrival, silently, with no action from her. The ten days give roughly one week of overlap so nothing vanishes between one delivery and the next.
- Size is hard-capped at 5 items per delivery (D-18). This replaces the original "whatever arrived, arrived," which was written before arrival volume was known and which F-04 falsified: at 180–280 candidate items per week, an uncontrolled Lane A is a wall, and a wall is the disease this system exists to treat.
- What is not surfaced is recorded (D-19), because a cap of 5 discards most of what arrives.
- Exactly two actions exist. **Keep** means "this one matters," and promotes the item into Lane B (D-07). **Less like this** records a negative relevance signal against the item's source, feeding the interest profile she can inspect and edit (D-10), and takes the item off the surface.
- There is no mark-read and no archive. Expiry is the default removal mechanism, and the only one that requires nothing from her.
- No related or suggested material appears here, ever.
- What expires unkept is recorded. That record is the evidence base for testing assumption A-01.

### 3.3 Lane B — Deliberate study

Current working behavior:

- Populated only by the Lane A gesture, or by hand.
- No cadence. Nothing arrives here on a schedule.
- No expiry. Items persist until she removes them.
- Hard cap on size. Adding past the cap requires removing something first.
- Actions available: notes, and marking done.
- This is the only surface where related material is offered, and only per item, on demand.

### 3.4 The relationship between lanes

**Confirmed by D-07.** Lane A feeds Lane B through the keep gesture. Nothing flows back. Lane A's job is to be forgettable; Lane B's job is to be persistent; and the gesture is the only bridge.

---

## 4. Decision ledger

This table is authoritative for whether a decision is settled.

| # | Decision | Firmness |
|---|---|---|
| D-01 | Two separated surfaces, current-awareness and deliberate study, rather than one combined feed. | **Confirmed** |
| D-02 | Items on Lane A expire on their own. Expiry, not action, is the default removal mechanism. | **Confirmed** |
| D-03 | Newsletter subscriptions live at `dagny099@gmail.com`, not the account already inventoried. | **Confirmed** |
| D-04 | That mailbox gets one discovery pass to learn what she already subscribed to. Email is a source of inspiration for the source list, not a runtime input to the system. | **Confirmed** |
| D-05 | Related content stays in scope. | **Confirmed** (she asked for it, naming TED talks as the example) |
| D-06 | Related content is confined to Lane B and never appears on Lane A. | **Confirmed** |
| D-07 | The Lane A keep gesture promotes the item into Lane B. | **Confirmed** |
| D-08 | Lane B is capped at **7**. Adding past the cap requires removing. | **Confirmed** 6 Sep 2026 |
| D-09 | Lane A arrives rather than waiting to be visited. | **Confirmed** |
| D-10 | Whatever decides relevance must be inspectable and editable by her: she can see what the system believes she cares about, see why an item surfaced, and change both. | **Confirmed** |
| D-11 | Any prioritization layer must beat a chronological baseline on a hand-labeled set, with the threshold written down in advance, or be removed. Removing it counts as a good outcome. | **Confirmed** 6 Sep 2026 |
| D-12 | Content pitched at beginners in retrieval, evaluation and knowledge graphs is treated as noise. | **Confirmed** |
| D-13 | Requirements and problem statement are maintained separately from any solutioning. | **Confirmed** |
| D-14 | Lane A has exactly two actions: keep, and "less like this" — a negative relevance signal against the source that also takes the item off the surface. No mark-read, no archive. | **Confirmed** |
| D-15 | Success criterion: the median time from keep to done on Lane B is 14 days or less. Judged only once at least three items have been marked done. | **Confirmed** |
| D-16 | Metrics may only be derived from gestures that exist for Barbara's own reasons. No gesture exists solely to produce a measurement. | **Confirmed** |
| D-17 | Encouragement is a retrospective, additive record of completed Lane B items. Never a streak, counter, badge, or deadline, and never on Lane A. | **Confirmed** |
| D-18 | One Lane A delivery is hard-capped at **5 items**, a fixed size rather than a relevance threshold or a per-source quota. | **Confirmed** 6 Sep 2026 |
| D-19 | What is never surfaced is recorded, alongside what expires unkept. Both are evidence, not features. | **Confirmed** 6 Sep 2026 |
| D-20 | Lane A arrives as a **recurring calendar event** carrying a link. Barbara creates that event by hand, once. Nothing automated writes to her calendar. | **Confirmed** 6 Sep 2026 |
| D-21 | The calendar event is a pointer, not a carrier: the delivery itself is a page reached by link, not content inside the message. | **Proposed** — Barbara said "probably a page"; not yet ratified |
| D-22 | Lane A carries pointers only. A kept item pulls its full text onto the Lane B shelf, so the reading arrives where the commitment is. | **Confirmed** 6 Sep 2026 |

D-11 exists because a ranked list always looks intelligent, and Barbara works in evaluation design. The deletability of the prioritization layer is a product decision, not a technical one, and it should survive into whatever gets built.

**What D-11 tests, stated narrowly (v1.9).** The held-out set covers everything field-adjacent in its window, promotional and automated mail included — Barbara set that inclusion rule on 6 Sep 2026. So D-11 asks whether a ranking beats reverse-chronological *at ordering field-adjacent candidates, promotional filtering included*. It does not test where the field boundary belongs (question 11), how a Source is identified when the sender is not the publication (question 12), or which delivery addresses count (question 10).

Note which way the inclusion rule cuts. Including promotional mail makes the chronological baseline **weaker**, not stronger: two of its top five are now a webinar promotion and an automated paper recommendation. Clearing that bar is a lower bar, and a ranker that merely declines to surface marketing will pass without demonstrating any judgment about relevance. The threshold under D-11 has to be set with that in mind, or the test will certify a ranker that has not earned its place — which is exactly the "prioritisation is theater" risk in Section 9.

D-15 is a latency measure rather than a count because promotion is the *save* gesture: under the failure mode described in F-03, a promotion count rises as the system stops working. Latency degrades in the correct direction, cannot be inflated by keeping more or keeping less, is readable after two or three items rather than after a month, and creates no recurring deadline — which matters because D-02 makes absence free, and a weekly pass/fail would quietly take that back.

D-16 is the durable guard. It is what should stop a later session from helpfully adding a "mark as read" control in order to make some number easier to compute. The test it encodes: a metric derived from a gesture Barbara would make anyway is safe; a metric requiring a gesture she would only make to feed the metric is the disease.

D-18's number is derived, not chosen by taste. D-15 requires a median keep-to-done of 14 days or less into a shelf of 7 (D-08). To finish roughly two items inside 14 days, Barbara can afford to keep one or two per delivery. A delivery of 5 at a realistic keep rate of 20–40% produces exactly that; a delivery of 20 produces four to eight keeps, overflows the shelf, and makes D-15 unreachable by construction. The cap is what makes the ratified success criterion achievable.

Fixed size, rather than a relevance threshold, is also what keeps D-11 testable: "did the ranker pick the right 5?" can be hand-labelled against a chronological top 5, whereas a variable-size threshold compares sets of different sizes. And a constant size is what keeps absence free under D-02 — a heavy week must not produce a pile.

D-20 was decided against Barbara's own measured data rather than by preference. D-09 requires that Lane A *arrive*, which needs a channel she already opens without deciding to, and that is not poisoned by backlog. Every mailbox she owns fails both tests: `dagny099@gmail.com` is 90.6% unread, `B@B` is 66% unread, `barbs@geocue.me` is 88% unread (F-02, F-07). A calendar passes both — it is opened daily as a matter of course, and a past event that went unopened recedes rather than accumulating as debt. That second property is D-02's "absence is free" enforced by the medium instead of by discipline.

The event is created **by Barbara, by hand, once**, and nothing automated touches her calendar. That is possible only because the event carries a stable link rather than the week's content, so it never needs updating. Any future automation of her calendar is a separate decision to be taken deliberately, not a convenience to drift into.

The falsifier, fixed in advance: run three deliveries and count opens. **Fewer than two of three means the channel is wrong, not the content.**

**Done, 7 Sep 2026.** Barbara created the event by hand: *Current-Depth Review Time!*, 8:00pm CT, recurring weekly on **Monday** and again on **Wednesday**, carrying the stable artifact link in its description. D-09 is now in force — the delivery arrives rather than waiting to be remembered — and A-10's three-delivery count can begin.

The two-event split was hers and is better than a single event would have been, because the two jobs are different lengths. **Monday is Lane A**, the five-minute skim of a new delivery. **Wednesday is Lane B**, the hour where something gets finished. That gives the *done* gesture a recurring moment of its own, which is precisely what A-08 doubts will happen unprompted — and it does so without the system imposing anything, because she scheduled it. D-17's ban on deadlines is not touched: a reminder she wrote herself is not a deadline the product created.

D-22 answers question 14 without re-creating the disease. Embedding five full articles in Lane A would put perhaps 15,000–20,000 words on one page: D-18's cap controls how many things arrive, not how long they are, so a wall would return in a different dimension. Confining full text to Lane B also avoids reproducing paywalled work in bulk — Pragmatic Engineer and Lenny's are paid — and keeps the click landing with the writer for anything merely skimmed. It falls out of the lane split rather than being bolted on: Lane A is the skim, Lane B is the hour.

Two costs are accepted knowingly. Text extraction keeps prose and loses figures, so items whose substance is a diagram or benchmark table degrade on the shelf and must keep a link alongside. And embedded text is a snapshot that cannot show a later correction.

**Delivery 001 predates D-22 and does not satisfy it.** It was built earlier the same day this decision was ratified, and it addresses every item by Gmail thread id — so the reading still happens inside the container Section 1.1 identifies as the defect, and the shelf holds a pointer rather than text. That is a limitation of the first delivery, not a revision of D-22. Delivery 002, 7 Sep 2026, is the first to carry canonical public URLs with text embedded at build time.

**D-22 is partly satisfiable, and the ceiling is set by the publishers.** Measured across Delivery 002's five items: one carried the whole article (Juan Sequeda, a free publication); three carried the opening section only before a paywall (Ken Huang, Beyond Euclid, Nate's Newsletter); one carried nothing at all. That last case is HackerNoon, whose digest publishes no canonical article link — only per-subscriber tracking redirects, so embedding one would place a token identifying Barbara inside the page. It falls back to Gmail, and the page says so.

So "the reading arrives where the commitment is" holds for roughly one item in five, partially for most, and not at all for some. This is a real constraint rather than an implementation gap, and it is the input to any later question about paid subscriptions or full-text fetching. It does not weaken the decision: an opening section on the shelf is still better than a link into a 90%-unread mailbox.

D-19 exists because D-18 discards roughly 97% of arriving items unseen. That makes the prioritisation layer load-bearing from the first delivery, which is precisely the "prioritisation is theater" risk in Section 9. Recording what was dropped is what lets D-11 be tested against the discarded material rather than only against what was shown.

D-19 does not say at what granularity, and Delivery 001 read it as aggregate disclosure. Whether "recorded" means item-level evidence is now question 15. The decision stands either way; only its granularity is open.

Three secondary diagnostics accompany D-15. They are **not** success criteria and must not be promoted into them:

- **Keep-to-done conversion.** Keeping eight and finishing one means the digest is too broad or the shelf too large. This is the evidence base the open D-08 cap question currently lacks.
- **Expiry Record** (Section 3.2), testing A-01.
- **Hide-to-keep ratio**, the tripwire for A-09.

**First evidence, 7 Sep 2026 — D-18's keep-rate assumption looks wrong.** Across the first ten surfaced items Barbara kept seven, a rate near **70%** against the 20–40% D-18's arithmetic assumed, and the shelf reached its cap of 7 on day one. At 70% a delivery of five produces about 3.5 keeps per cycle, which saturates a 7-slot shelf within a fortnight and holds it there unless roughly 3.5 items are finished per week.

Both caps were held fixed on 7 Sep rather than adjusted, deliberately: at n=10, moving two numbers at once would make any subsequent change unattributable. Three readings remain open — the picks are good and the delivery should be *smaller*; or the bar for keeping is too low because Delivery 001 gave no way to judge an item without opening Gmail, making "keep" mean *deal with this later*, which is the F-03 failure mode; or both. The next cycle discriminates, because Delivery 002 is the first where an item's text can be skimmed before committing. Full numbers and caveats in `docs/evals/pilot-log.md`.

---

## 5. Non-goals

Established, not inferred.

| Not this | Reason |
|---|---|
| Inbox cleanup | Adjacent and tempting. Different project. Doing it would produce no reading by itself. |
| Comprehensive coverage | Missing things is expected and acceptable. Completeness is the impulse that produces volume, and volume is the disease. |
| A system of record for everything she reads | This handles one stream she currently misses. Nothing more. |
| A product for anyone else | Single user. No accounts, no sharing, no generality tax. |
| Replacing an existing tool | She is not using one. Nothing to migrate. |
| Read/unread state, archive | Designed out deliberately. Their absence is the differentiating decision, not an omission to be helpfully filled in later. The "less like this" signal (D-14) is not a read-state: it expresses a judgment about the content rather than tracking whether she has consumed it. |
| Runtime access to her mailbox | Email appears once, for source discovery. The running system does not read her mail. |

---

## 6. Assumptions

Each is a place where the design rests on inference. None has been validated against Barbara's behavior.

| # | Assumption | Basis | How it could be tested |
|---|---|---|---|
| A-01 | Expiry suits her. Queues she keeps would rot. | Category history (F-03), not her data. | Record what expires unkept for a month. If she repeatedly wishes she still had something, the assumption is wrong. |
| A-02 | Weekly is the right Lane A cadence. **Still an assumption; deliveries land Mondays.** | Never affirmatively chosen — it was inherited and then used. The first evidence pushes against it: at the observed keep rate, five items a week saturate the shelf (see the D-18 note in Section 4). The live alternative is three items twice weekly — same throughput, faster rhythm, and it fits Barbara's stated impatience with week-long waits. | Living with it. **Do not confuse delivery cadence with review cadence:** deliveries are weekly, while Barbara's own calendar prompts are twice weekly, Monday and Wednesday. Two events per week is not evidence of two deliveries per week. |
| A-03 | Ten days is the right expiry window. | Derived from A-02, to give one week of overlap. | Falls with A-02. |
| A-04 | She is past introductory material in retrieval, evaluation and knowledge graphs. | Her stated background. | High confidence. |
| A-05 | Enterprise data management sources are vendor-dominated with a low signal rate and need different handling from the ML sources. **Confirmed 6 Sep 2026.** *(Briefly and wrongly retired in v1.3 on the strength of the retracted F-06; reinstated in v1.4.)* | Now checked against her actual subscriptions. DATAVERSITY sends roughly 5 messages per week, overwhelmingly webinar, conference and CDMP-certification promotion — "Join Us", "Register now", "Early Bird" — with editorial appearing mainly inside The DATAVERSITY Download and occasional white papers. ODSC follows the same shape: a genuine weekly article roundup wrapped in conference marketing. | Already tested. Holds, and it is the clearest case in the source list for treating a source's editorial content differently from its promotional content. |
| A-06 | The measured clutter in the other mailbox represents the deterrent effect she described. | Corroboration only. Causation not established. **Weakened 6 Sep 2026:** F-07 shows the real mailbox is heavily organised and filtered, and its newsletters still go 98% unread. Clutter cannot be the whole mechanism. | Would require observing her behavior, not her mailbox. Probably not worth testing. |
| A-07 | There is enough arriving to justify a prioritization layer. **Confirmed 6 Sep 2026** by the discovery pass: 40–50 field-adjacent messages per week, 150–250 candidate items. | F-04, now closed. | Already tested. Holds. |
| A-08 | She will mark `done` on Lane B reliably enough for D-15's latency to mean anything. | Inference, not observation. Plenty of people finish the article and never tap the button. | After one month, compare the done count against her own recollection of what she actually finished. A large gap invalidates D-15 rather than her reading. |
| A-09 | Taking items off Lane A via "less like this" will not turn Lane A into a surface she clears. | Judgment. She chose hiding over signal-only in v1.2 with the clearing risk stated. **Early reading 7 Sep 2026: hide-to-keep is 0 : 7.** The tripwire is not firing, but it is firing *in reverse* — she keeps nearly everything and hides nothing, which is a different problem and the one D-18's keep-rate note addresses. | Hide-to-keep ratio per delivery cycle. If hides run well ahead of keeps, Lane A has become a list to clear, and the correct response is a narrower digest, not a better hide control. A ratio near zero in the other direction means the digest is not discriminating, or that keeping is standing in for judging. |
| A-10 | A calendar is a channel Barbara actually opens, and a past unopened event recedes rather than accumulating as debt. **Added v1.9. Now under live test — the event exists as of 7 Sep 2026.** | Inference about her behaviour, not measurement. It sits inside D-20's rationale, where it was easy to mistake for something that had been checked. Naming it does not weaken D-20: that decision was taken against measured mailbox data, and this assumption is the part of the reasoning that was *not* measured. | Falsifier fixed in advance under D-20: run three deliveries and count opens. Fewer than two of three means the channel is wrong, not the content. **Opens are counted per delivery cycle, not per event** — there are two events a week and one delivery, so an open on either counts once. Counting creates no new gesture; a page load is something she does for her own reasons, so D-16 is satisfied. |

A-07 was the one that could have collapsed a large part of this design. It did not: volume is high, so chronological order is not sufficient and the prioritisation layer is justified. D-11's deletability test still applies — the layer must earn its place — but it is now worth building and testing rather than skipping.

The risk has inverted. The open problem is no longer "is there enough to rank?" but "there is far too much," which is what question 9 now asks.

---

## 7. Unresolved product questions

Ordered by how much they block.

1. **What is actually arriving?** **Resolved 6 Sep 2026 — see F-04 through F-07.** Question text kept so the record survives.
2. **What outcome would she notice?** **Resolved in v1.2 — see D-15, D-16, D-17.** Question text kept so the record of what was open survives. The answer landed on a latency criterion (median keep to done, 14 days) rather than a count, because a count of promotions rises in the failure mode; on a rule governing which gestures may be measured at all; and on encouragement being a growing record of finished items rather than a streak.
3. **Does enterprise data management belong in scope?** **Resolved 6 Sep 2026: yes.** Barbara confirmed it after the corrected source list showed she is in fact subscribed — DATAVERSITY, ODSC, the Knowledge Graph Conference, and the LinkedIn metadata/ontology stream. The original sub-question, job-driven or interest-driven, was not asked and remains open, but it no longer blocks: the sources exist either way. What A-05 adds is that this field needs different handling from the ML sources, because its editorial content is buried inside promotional mail.
4. **How does Lane A arrive?** **Resolved 6 Sep 2026 — a recurring calendar event, see D-20.** All three candidates originally listed here turned out to be broken: a bookmark is fetched rather than arrived, which contradicts D-09; and a message to herself lands in the very container Section 1.1 identifies as the defect, in a mailbox that is 90.6% unread. The candidate list was incomplete, not merely undecided.
5. **What is the Lane B cap, exactly?** **Resolved 6 Sep 2026: seven.** Ratified together with D-08, on the strength of the D-18 arithmetic, which uses 7. *(Note the circularity: D-18's arithmetic was derived from a shelf of 7, so it cannot independently justify 7.)* **Reopened as an observation, not a decision, 7 Sep 2026:** the shelf filled on day one and Keep is now disabled on every live item. Barbara considered making the cap configurable and decided against it — the cap is the mechanism, and a cap that can be raised when it binds is a suggestion. Both caps stay fixed while a second cycle of evidence accrues. See `docs/evals/pilot-log.md`.
6. **Does expiry survive contact with her habits?** A-01 is argued from category history rather than from her behavior. If she has a counterexample from her own life, that outranks anything cited here.
7. **What is the gesture called?** "Favorite" and "keep" were both used for the same action.
8. **How far does related content extend?** TED talks were the stated example. Whether it covers papers, conference talks, or other media was never scoped.

Added in v1.3, from the discovery pass:

9. **How big is one Lane A delivery?** **Resolved 6 Sep 2026: five, hard-capped — see D-18 and D-19.** The answer turned out to be both of the options this question offered: a hard size limit *and* a load-bearing prioritisation layer, because a cap of 5 against 180–280 arriving items cannot avoid making the ranker load-bearing. Cadence remains open under A-02; the cap is per delivery whatever the cadence turns out to be.
10. **Which addresses count as sources?** F-05 found **six** delivery addresses in one mailbox, with the same publication arriving twice. Deduplication is required. Which of the six are in scope is Barbara's call.
11. **Is "field-adjacent" defined by her subscriptions or by her intent?** **Narrowed in v1.4.** With F-06 retracted, her subscriptions and Section 1's three named fields agree far better than v1.3 claimed — all three fields are represented. What remains is the non-field stream sharing the same labels (military analysis, cooking, games, fiction, public health) and the promotional share of the vendor sources. D-12 already treats beginner content as noise; this asks the prior question of what counts as signal. Barbara has named DeepLearning.AI as a high-quality reference point, which is a usable anchor for that judgment.
12. **What is a Source, when the sender address is not the publication?** All LinkedIn newsletters — the metadata/ontology stream, The AI Agent Report, The AI Table Review, MIT CSAIL — arrive from the single address `newsletters-noreply@linkedin.com`. Sender-based source identity fails here. Raised by the v1.4 pass; not yet discussed.

Added in v1.7, from the delivery-mechanism decision:

13. **Where does the page live?** The link in D-20's calendar event has to point somewhere stable. Currently an Anthropic-hosted Artifact, which costs nothing and gives cross-device state for free. Barbara owns `balex.com` and asked about her own infrastructure. The trade-off is specific and worth stating before choosing: **self-hosting a static page is easy; re-solving synced state is not.** The prototype persists through the Artifact runtime when published and falls back to browser-local storage otherwise, so a self-hosted copy would be per-device until something replaces that. Choosing a host is tool selection, which Section 0 still places outside scope until Barbara opens the architecture phase.
14. **Does the delivery carry the reading, or only point at it?** **Resolved 6 Sep 2026 — see D-22.** Neither extreme. Lane A links out, and Gmail is bypassed by pointing at each item's public web version rather than the message; the canonical URL is extractable from the message body, and nearly every source publishes one. Full text is pulled only when an item is kept.

Added in v1.9, from the Codex review adjudication:

15. **What granularity does D-19 require — the record, or the disclosure?** D-19 says what is never surfaced is *recorded*. Delivery 001 *discloses* it as five aggregate buckets. Those are arguably two different obligations, and the brief does not distinguish them. The proposal, which needs Barbara's nod rather than an agent's: the **record** is item-level and lives in the repo, where it can be argued with and reused (`docs/evals/held-out-2026-08-24.md` is already exactly this shape); the **disclosure** is the aggregate summary on the delivery page, and stays aggregate, because a list of 197 rejected items on the page would rebuild the wall D-18 exists to prevent. If that split is right, scope the record to field-adjacent candidates — roughly 30–40 a week — rather than all ~200, since the general-inbox remainder is not what D-11 will ever be tested against. **Unresolved.** Until it is settled, do not claim Delivery 001 either satisfies or violates D-19.

---

## 8. Candidate concepts and entities

This is a **vocabulary sketch, not a settled domain model**. It exists to make product discussion concrete without choosing storage, schema, field types, or architecture.

As of v1.10 only D-21 remains `Proposed`. Several concepts below still rest on assumptions, chiefly A-07 and A-08. Their appearance here does **not** upgrade any status.

| Concept | What it represents | Status / dependency |
|---|---|---|
| **Source** | A publication Barbara may choose to follow. | Observed candidate set now recorded in Section 1.5. Which of them are in scope depends on question 11. A Source may deliver to more than one address (F-05). |
| **Item** | One piece of content from a Source. | Conceptually useful. |
| **Lane A Placement** | An Item present in the current-awareness surface. | Lane A expiry itself is confirmed by D-02; exact cadence / timing remain assumption-dependent (A-02, A-03). |
| **Keep gesture** | The gesture signalling that an Item matters. | Promotes into Lane B per D-07, Confirmed. Name still unresolved (question 7); the brief writes **keep**. |
| **Lane B Entry** | An Item in the deliberate-study surface, with notes and done state. | Done is load-bearing rather than merely available: D-15 measures the interval between keep and done. Capped at 7 by D-08, Confirmed. |
| **Completion** | A Lane B Entry marked done, carrying both the keep time and the done time. | The interval is what D-15 measures. Depends on A-08 holding. |
| **Completion Record** | The retrospective, additive list of Completions. | The encouragement artifact under D-17. Additive only; never a streak or counter. |
| **Negative Signal** | A "less like this" event against an Item's Source. | Depends on D-14. Feeds the Interest Profile under D-10. |
| **Interest Profile** | A readable / editable statement of what Barbara cares about. | Required by D-10, Confirmed. A-07 holds, so it is warranted. |
| **Relevance Judgment** | A relevance result plus a human-readable reason. | Required by D-10; must survive D-11's delete-or-keep test, both Confirmed. |
| **Expiry Record** | A record of what left Lane A without being kept, and of what was never surfaced. | Required by D-19, Confirmed. Evidence for A-01. |
| **Related Suggestion** | Additional material associated with an item selected for deeper study. | In scope by D-05, confined to Lane B by D-06, both Confirmed. Breadth still open (question 8). |
| **Reading Text** | The extracted article text of a kept item, held on the Lane B shelf. | D-22, Confirmed. Absent from Lane A. Figures are lost in extraction, so a link is kept alongside. |
| **Arrival** | The recurring calendar event carrying the link to a delivery. | D-20, Confirmed. Created by Barbara by hand; carries no content, so it never goes stale. Whether the link's destination is a page rather than the content itself depends on D-21, still Proposed. |

Two relationships that were conditional in earlier versions are now settled:

- **Lane A → Lane B promotion** — Confirmed by D-07.
- **Related suggestions only in Lane B** — Confirmed by D-06. How far "related" extends is still open (question 8).

---

## 9. Known risks

Carried forward because they should inform product decisions, not just engineering ones.

- **It becomes a fourth place not to read.** Three surfaces already go unread. This is the default outcome for a project like this. The expiry design and the arrives-not-fetched decision are the mitigations.
- **The prioritisation layer is theater.** Plausible reasons attached to arbitrary ordering are indistinguishable from real relevance by inspection. D-11 exists for this.
- **Building it replaces reading.** The sharpest risk and specific to Barbara, who enjoys building. The project can succeed technically and still fail the actual goal of reading more. Any plan that puts a long build before a first working delivery is making this risk worse.

---

## 10. What a receiving agent should do first

Not architecture. In order:

**As of v1.10, twenty-one of twenty-two decisions are Confirmed; only D-21 is Proposed.** Questions 1, 2, 3, 4, 5, 9 and 14 are closed; 15 is open. Two deliveries are live, they arrive through a calendar event, and the first cross-harness review is done. The decision ledger is not the bottleneck, and has not been for three revisions — evidence is.

This section was rewritten in v1.9 because every item in the v1.8 version had gone stale: the pilot had stopped being manual, the corpus had been captured, and the review it pointed forward to had already happened. Read that as a warning about this section in particular — it dates faster than the rest of the brief.

The sequenced plan lives in `docs/plans/2026-09-06-product-clarification-plan.md`. In outline, what is actually next:

1. **Keep delivering, and watch the keep rate.** Deliveries 001 and 002 are live; the design pass is done; the calendar event exists. **Delivery 003 lands Monday 14 Sep.** The open question the next cycle answers is whether the ~70% keep rate is real or an artifact of Delivery 001's poor affordances — that determines whether the delivery should shrink to three twice-weekly. Nothing else should be changed until it does. Record everything in `docs/evals/pilot-log.md`.
2. **Close the cheap product questions as they come up in the building** — 7, 8, 10, 11, 12, 15, and A-02 with A-03. Propose an answer, get her nod, move on. Do not run a separate question-closing exercise, and do not let an open question stop work that does not depend on it.
3. **Label the D-11 held-out set when she has the appetite.** The corpus is complete and ready (`docs/evals/held-out-2026-08-24.md`): 62 units across 24–30 Aug. It decides whether a ranking layer survives. **It is not a prerequisite for building one, or for anything else.** Nothing waits on it.
4. **Work the adjudicated review findings.** The Codex review of v1.8 and its adjudication both live in `docs/reviews/`. Open items are tracked there rather than duplicated here.

Only then does architecture become a sensible next step, and only on Barbara's explicit say-so.
