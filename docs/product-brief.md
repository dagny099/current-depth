# Reading Digest — Product Brief

**Version** 1.6 · 6 Sep 2026
**Owner** Barbara (single user; this is a personal system, not a product)
**Status** Pre-architecture, but no longer nothing-built: Delivery 001 is running at `prototype/current-depth.html`. Every decision in the ledger is Confirmed. What remains is evidence, a handful of cheap questions, and the D-11 evaluation.

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

Originally requested by Barbara, retained for the record:

- Do not design the technical architecture. No storage design, no pipeline topology, no tool or vendor selection. **Still binding.**
- ~~Do not implement anything.~~ **Retired 6 Sep 2026.**
- Do not fill gaps with new product ideas. Where this brief says a question is unresolved, it is unresolved, and inventing an answer destroys the record of what was actually decided. **Still binding.**

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

**Working experience sketch — not a decision ledger.** This section intentionally includes behaviors that are still `Proposed` or assumption-dependent. Use Section 4 and Section 6 to determine what is actually settled.

Written from Barbara's side of the screen.

Once a week, something arrives carrying a handful of things worth knowing about in her fields. She reads it or she does not. If she does not, nothing happens: no counter climbs, no badge appears, nothing waits for her. The items age out on their own within days and leave no residue. Ignoring it for three weeks costs nothing and leaves the system in a good state.

When something in that weekly arrival is worth more than a skim, she makes **one gesture**. That is the only action available. The item moves onto a small shelf that does not expire and does not grow past its cap. The shelf is where she goes when she has an hour rather than five minutes, and it is the only place the system ever offers her additional material — a related talk, a related paper — because offering more things to read in the weekly stream would be the disease, not the treatment.

The shelf being capped is the mechanism, not a limitation. Adding a new item when it is full requires removing one, which forces a choice she would otherwise defer indefinitely.

Nothing in this experience involves archiving, marking read, or clearing a list. Those actions are absent by design. She can tell the system "less like this," which teaches it and takes the item off the surface, but that is a judgment about the content rather than housekeeping. Disappearance remains the default state, and attention is the only thing that overrides it.

---

## 3. Lane A and Lane B

**Working model — not all details are confirmed.** This section preserves the current design concept in one place. If a detail here is `Proposed`, assumed, or unresolved elsewhere, that status still governs.

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

- Arrives on a weekly cadence. Barbara does not fetch it. A destination she must remember to visit is a destination she will stop visiting.
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

**Working design; depends on D-07.** Lane A feeds Lane B through the single gesture. Nothing flows back. Lane A's job is to be forgettable; Lane B's job is to be persistent; and the gesture is the only bridge.

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

D-11 exists because a ranked list always looks intelligent, and Barbara works in evaluation design. The deletability of the prioritization layer is a product decision, not a technical one, and it should survive into whatever gets built.

D-15 is a latency measure rather than a count because promotion is the *save* gesture: under the failure mode described in F-03, a promotion count rises as the system stops working. Latency degrades in the correct direction, cannot be inflated by keeping more or keeping less, is readable after two or three items rather than after a month, and creates no recurring deadline — which matters because D-02 makes absence free, and a weekly pass/fail would quietly take that back.

D-16 is the durable guard. It is what should stop a later session from helpfully adding a "mark as read" control in order to make some number easier to compute. The test it encodes: a metric derived from a gesture Barbara would make anyway is safe; a metric requiring a gesture she would only make to feed the metric is the disease.

D-18's number is derived, not chosen by taste. D-15 requires a median keep-to-done of 14 days or less into a shelf of 7 (D-08). To finish roughly two items inside 14 days, Barbara can afford to keep one or two per delivery. A delivery of 5 at a realistic keep rate of 20–40% produces exactly that; a delivery of 20 produces four to eight keeps, overflows the shelf, and makes D-15 unreachable by construction. The cap is what makes the ratified success criterion achievable.

Fixed size, rather than a relevance threshold, is also what keeps D-11 testable: "did the ranker pick the right 5?" can be hand-labelled against a chronological top 5, whereas a variable-size threshold compares sets of different sizes. And a constant size is what keeps absence free under D-02 — a heavy week must not produce a pile.

D-19 exists because D-18 discards roughly 97% of arriving items unseen. That makes the prioritisation layer load-bearing from the first delivery, which is precisely the "prioritisation is theater" risk in Section 9. Recording what was dropped is what lets D-11 be tested against the discarded material rather than only against what was shown.

Three secondary diagnostics accompany D-15. They are **not** success criteria and must not be promoted into them:

- **Keep-to-done conversion.** Keeping eight and finishing one means the digest is too broad or the shelf too large. This is the evidence base the open D-08 cap question currently lacks.
- **Expiry Record** (Section 3.2), testing A-01.
- **Hide-to-keep ratio**, the tripwire for A-09.

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
| A-02 | Weekly is the right Lane A cadence . | Never discussed. PLEASE HELP ME THINK THROUGH THIS. | Ask. Cheap to change before anything exists. |
| A-03 | Ten days is the right expiry window. | Derived from A-02, to give one week of overlap. | Falls with A-02. |
| A-04 | She is past introductory material in retrieval, evaluation and knowledge graphs. | Her stated background. | High confidence. |
| A-05 | Enterprise data management sources are vendor-dominated with a low signal rate and need different handling from the ML sources. **Confirmed 6 Sep 2026.** *(Briefly and wrongly retired in v1.3 on the strength of the retracted F-06; reinstated in v1.4.)* | Now checked against her actual subscriptions. DATAVERSITY sends roughly 5 messages per week, overwhelmingly webinar, conference and CDMP-certification promotion — "Join Us", "Register now", "Early Bird" — with editorial appearing mainly inside The DATAVERSITY Download and occasional white papers. ODSC follows the same shape: a genuine weekly article roundup wrapped in conference marketing. | Already tested. Holds, and it is the clearest case in the source list for treating a source's editorial content differently from its promotional content. |
| A-06 | The measured clutter in the other mailbox represents the deterrent effect she described. | Corroboration only. Causation not established. **Weakened 6 Sep 2026:** F-07 shows the real mailbox is heavily organised and filtered, and its newsletters still go 98% unread. Clutter cannot be the whole mechanism. | Would require observing her behavior, not her mailbox. Probably not worth testing. |
| A-07 | There is enough arriving to justify a prioritization layer. **Confirmed 6 Sep 2026** by the discovery pass: 40–50 field-adjacent messages per week, 150–250 candidate items. | F-04, now closed. | Already tested. Holds. |
| A-08 | She will mark `done` on Lane B reliably enough for D-15's latency to mean anything. | Inference, not observation. Plenty of people finish the article and never tap the button. | After one month, compare the done count against her own recollection of what she actually finished. A large gap invalidates D-15 rather than her reading. |
| A-09 | Taking items off Lane A via "less like this" will not turn Lane A into a surface she clears. | Judgment. She chose hiding over signal-only in v1.2 with the clearing risk stated. | Hide-to-keep ratio per delivery cycle. If hides run well ahead of keeps, Lane A has become a list to clear, and the correct response is a narrower digest, not a better hide control. |

A-07 was the one that could have collapsed a large part of this design. It did not: volume is high, so chronological order is not sufficient and the prioritisation layer is justified. D-11's deletability test still applies — the layer must earn its place — but it is now worth building and testing rather than skipping.

The risk has inverted. The open problem is no longer "is there enough to rank?" but "there is far too much," which is what question 9 now asks.

---

## 7. Unresolved product questions

Ordered by how much they block.

1. **What is actually arriving?** **Resolved 6 Sep 2026 — see F-04 through F-07.** Question text kept so the record survives.
2. **What outcome would she notice?** **Resolved in v1.2 — see D-15, D-16, D-17.** Question text kept so the record of what was open survives. The answer landed on a latency criterion (median keep to done, 14 days) rather than a count, because a count of promotions rises in the failure mode; on a rule governing which gestures may be measured at all; and on encouragement being a growing record of finished items rather than a streak.
3. **Does enterprise data management belong in scope?** **Resolved 6 Sep 2026: yes.** Barbara confirmed it after the corrected source list showed she is in fact subscribed — DATAVERSITY, ODSC, the Knowledge Graph Conference, and the LinkedIn metadata/ontology stream. The original sub-question, job-driven or interest-driven, was not asked and remains open, but it no longer blocks: the sources exist either way. What A-05 adds is that this field needs different handling from the ML sources, because its editorial content is buried inside promotional mail.
4. **How does Lane A arrive?** D-09 says it arrives rather than being fetched. The mechanism was not settled. Candidates discussed: a message to herself, a bookmarked destination, or a message linking to a destination. The argument for a message is that it borrows a habit she already has instead of asking her to form one.
5. **What is the Lane B cap, exactly?** **Resolved 6 Sep 2026: seven.** Ratified together with D-08, on the strength of the D-18 arithmetic, which uses 7.
6. **Does expiry survive contact with her habits?** A-01 is argued from category history rather than from her behavior. If she has a counterexample from her own life, that outranks anything cited here.
7. **What is the gesture called?** "Favorite" and "keep" were both used for the same action.
8. **How far does related content extend?** TED talks were the stated example. Whether it covers papers, conference talks, or other media was never scoped.

Added in v1.3, from the discovery pass:

9. **How big is one Lane A delivery?** **Resolved 6 Sep 2026: five, hard-capped — see D-18 and D-19.** The answer turned out to be both of the options this question offered: a hard size limit *and* a load-bearing prioritisation layer, because a cap of 5 against 180–280 arriving items cannot avoid making the ranker load-bearing. Cadence remains open under A-02; the cap is per delivery whatever the cadence turns out to be.
10. **Which addresses count as sources?** F-05 found at least three delivery addresses in one mailbox, with the same publication arriving twice. Deduplication is required. Whether all three addresses are in scope is Barbara's call.
11. **Is "field-adjacent" defined by her subscriptions or by her intent?** **Narrowed in v1.4.** With F-06 retracted, her subscriptions and Section 1's three named fields agree far better than v1.3 claimed — all three fields are represented. What remains is the non-field stream sharing the same labels (military analysis, cooking, games, fiction, public health) and the promotional share of the vendor sources. D-12 already treats beginner content as noise; this asks the prior question of what counts as signal. Barbara has named DeepLearning.AI as a high-quality reference point, which is a usable anchor for that judgment.
12. **What is a Source, when the sender address is not the publication?** All LinkedIn newsletters — the metadata/ontology stream, The AI Agent Report, The AI Table Review, MIT CSAIL — arrive from the single address `newsletters-noreply@linkedin.com`. Sender-based source identity fails here. Raised by the v1.4 pass; not yet discussed.

---

## 8. Candidate concepts and entities

This is a **vocabulary sketch, not a settled domain model**. It exists to make product discussion concrete without choosing storage, schema, field types, or architecture.

Some concepts below depend on `Proposed` decisions or assumptions. Their appearance here does **not** make those decisions confirmed.

| Concept | What it represents | Status / dependency |
|---|---|---|
| **Source** | A publication Barbara may choose to follow. | Observed candidate set now recorded in Section 1.5. Which of them are in scope depends on question 11. A Source may deliver to more than one address (F-05). |
| **Item** | One piece of content from a Source. | Conceptually useful. |
| **Lane A Placement** | An Item present in the current-awareness surface. | Lane A expiry itself is confirmed by D-02; exact cadence / timing remain assumption-dependent (A-02, A-03). |
| **Keep / Favorite gesture** | The single gesture discussed for signaling that an Item matters. | Name unresolved. Promotion into Lane B depends on proposed D-07. |
| **Lane B Entry** | An Item in the deliberate-study surface, with notes and done state. | Done is now load-bearing rather than merely available: D-15 measures the interval between keep and done. Cap still depends on proposed D-08. |
| **Completion** | A Lane B Entry marked done, carrying both the keep time and the done time. | The interval is what D-15 measures. Depends on A-08 holding. |
| **Completion Record** | The retrospective, additive list of Completions. | The encouragement artifact under D-17. Additive only; never a streak or counter. |
| **Negative Signal** | A "less like this" event against an Item's Source. | Depends on D-14. Feeds the Interest Profile under D-10. |
| **Interest Profile** | A readable / editable statement of what Barbara cares about. | Depends on proposed D-10 and may be unnecessary if A-07 fails. |
| **Relevance Judgment** | A relevance result plus a human-readable reason. | Depends on proposed D-10 / D-11 and on enough volume existing to justify prioritisation (A-07). |
| **Expiry Record** | A record of what left Lane A without being kept. | Candidate evidence mechanism for testing A-01; not independently confirmed as a requirement. |
| **Related Suggestion** | Additional material associated with an item selected for deeper study. | Related content is confirmed in scope by D-05; confinement to Lane B depends on proposed D-06. |

Two relationships are currently part of the working design but remain conditional:

- **Lane A → Lane B promotion** depends on D-07 being confirmed.
- **Related suggestions only in Lane B** depends on D-06 being confirmed.

---

## 9. Known risks

Carried forward because they should inform product decisions, not just engineering ones.

- **It becomes a fourth place not to read.** Three surfaces already go unread. This is the default outcome for a project like this. The expiry design and the arrives-not-fetched decision are the mitigations.
- **The prioritisation layer is theater.** Plausible reasons attached to arbitrary ordering are indistinguishable from real relevance by inspection. D-11 exists for this.
- **Building it replaces reading.** The sharpest risk and specific to Barbara, who enjoys building. The project can succeed technically and still fail the actual goal of reading more. Any plan that puts a long build before a first working delivery is making this risk worse.

---

## 10. What a receiving agent should do first

Not architecture. In order:

**As of v1.5 every decision in the ledger is Confirmed. Nineteen of nineteen.** Questions 1, 2, 3, 5 and 9 are closed. The decision ledger is no longer the bottleneck.

The sequenced plan lives in `docs/plans/2026-09-06-product-clarification-plan.md`. In outline:

1. **Run a manual pilot before building anything.** It tests A-01, A-02, A-08, A-09 and D-15 at zero build cost, and it is the only direct mitigation for the sharpest risk in Section 9 — that building the system replaces reading.
2. Close the remaining cheap product questions: 4, 7, 8, 10, 11, 12, and A-02 with A-03.
3. Build the D-11 evaluation set. Now ratified, D-11 requires a hand-labelled corpus and a written-in-advance threshold *before* any ranker exists. This is the critical path, and it needs mailbox access, so capture the corpus while the connector is still switched.
4. Then the cross-harness review the README describes, from a frozen brief.

Only then does architecture become a sensible next step, and only on Barbara's explicit say-so.
