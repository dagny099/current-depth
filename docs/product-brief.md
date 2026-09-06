# Reading Digest — Product Brief

**Version** 1.3 · 6 Sep 2026
**Owner** Barbara (single user; this is a personal system, not a product)
**Status** Pre-architecture. Handoff-ready for product clarification; nothing built. The brief contains confirmed decisions, proposed decisions, assumptions, and unresolved questions.

---

## 0. How to read this brief

You have no access to the conversation that produced this. This brief is intended to be self-contained for the next product-clarification work.

Two conventions matter:

**Every decision below is tagged with its firmness.** `Confirmed` means Barbara explicitly chose it. `Proposed` means it was put to her, went uncontested, and is written into the requirements, but she never affirmatively ratified it. Treat `Proposed` items as revisable on contact with her; do not treat them as settled just because they appear here.

**Assumptions are separated from decisions on purpose.** Several load-bearing parts of this design rest on inference rather than on Barbara's stated behavior. Those are listed in Section 6 with their basis. If you find yourself building something that depends on an assumption, surface it rather than hardening it.

**Status labels control.** Narrative prose, experience sketches, tables, and candidate entities may describe the current working design, but they do not upgrade firmness. When there is any tension, the decision ledger in Section 4 and the assumptions in Section 6 are authoritative for status.

### Out of scope for the next work

Explicitly requested by Barbara, and binding on you:

- Do not design the technical architecture. No storage design, no pipeline topology, no tool or vendor selection.
- Do not implement anything.
- Do not fill gaps with new product ideas. Where this brief says a question is unresolved, it is unresolved, and inventing an answer destroys the record of what was actually decided.

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
| F-04 | Arrival rate and composition at `dagny099@gmail.com`. **Resolved 6 Sep 2026** by a read-only discovery pass. Field-adjacent editorial arrives at roughly **40–50 messages per week**, carrying an estimated **150–250 candidate items per week**. Total mailbox arrival is far higher: 192,111 inbox messages, 174,073 unread (90.6%), and a one-day sample implies well over 100 threads per day. | **Closed.** Volume is high. |
| F-05 | The mailbox serves at least three addresses — `dagny099@gmail.com`, `barbs@balex.com`, `hidalgod@gmail.com` — and some publications deliver to two of them. Observed: the same `thebatch@deeplearning.ai` issue arriving twice, once per address. | **Holds.** Creates a deduplication requirement. |
| F-06 | The subscriptions do not match the fields named in Section 1. Observed field-adjacent sources are AI/LLM/agents and software-product engineering. **No enterprise data management sources were found** — no warehouse, catalog, governance, or data-quality publications. | **Holds.** Bears on A-05 and question 3. |
| F-07 | This mailbox is heavily organised — roughly 40 user labels, with working filters (`SubStack` 4,390 messages, `DL.ai` 667, `B@B` 23,532). It is the opposite of the unorganised mailbox measured in F-02, yet the unread rate is worse: the `SubStack` label alone is 4,317 unread of 4,390 (98.3%). | **Holds.** Filing happens; reading does not. |

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

**Vendor / course marketing rather than editorial:** `hello@deeplearning.ai`, `maven@list.maven.com`, and the Maven course senders. Low signal by the standard D-12 sets.

**Sharing the same labels but outside the named fields:** `ryanmcbeth` (military analysis, the single highest-volume sender observed), `whattocook` and `elliekrieger` (cooking), `stephentotilo` (games), `yourlocalepidemiologist` (public health), `georgesaunders` (fiction). These are not noise in the D-12 sense — they appear to be things she chose — but they are not the stated fields either. Question 11.

**Absent entirely:** enterprise data management. No warehouse, catalog, governance, lineage, or data-quality publication was found. See F-06.

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
| Size | Whatever arrived — **contested, see question 9** | Hard cap (7 or so) |
| Actions | Keep, less like this | Notes, done |
| Keep does | Promotes into Lane B | n/a |

Terminology note: "favorite" and "keep" refer to the same gesture. This brief now writes it as **keep** throughout for consistency, but the name is still unresolved (question 7) and using it here does not settle it.

The Actions row changed in v1.2. Lane A previously had one action; it now has two, per D-14.

### 3.2 Lane A — Current awareness

Current working behavior:

- Arrives on a weekly cadence. Barbara does not fetch it. A destination she must remember to visit is a destination she will stop visiting.
- Items expire approximately ten days after arrival, silently, with no action from her. The ten days give roughly one week of overlap so nothing vanishes between one delivery and the next.
- Size is uncontrolled: whatever arrived, arrived. **Contested by F-04 as of v1.3.** This was written when arrival volume was unknown. At 150–250 candidate items per week, an uncontrolled Lane A is a wall of text, which is the disease this system exists to treat. Left as written rather than silently amended; question 9 puts it to Barbara.
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
| D-08 | Lane B is capped. Adding past the cap requires removing. | **Proposed-Please help think through this** |
| D-09 | Lane A arrives rather than waiting to be visited. | **Confirmed** |
| D-10 | Whatever decides relevance must be inspectable and editable by her: she can see what the system believes she cares about, see why an item surfaced, and change both. | **Confirmed** |
| D-11 | Any prioritization layer must beat a chronological baseline on a hand-labeled set, with the threshold written down in advance, or be removed. Removing it counts as a good outcome. | **Proposed-Please help think through this** |
| D-12 | Content pitched at beginners in retrieval, evaluation and knowledge graphs is treated as noise. | **Confirmed** |
| D-13 | Requirements and problem statement are maintained separately from any solutioning. | **Confirmed** |
| D-14 | Lane A has exactly two actions: keep, and "less like this" — a negative relevance signal against the source that also takes the item off the surface. No mark-read, no archive. | **Confirmed** |
| D-15 | Success criterion: the median time from keep to done on Lane B is 14 days or less. Judged only once at least three items have been marked done. | **Confirmed** |
| D-16 | Metrics may only be derived from gestures that exist for Barbara's own reasons. No gesture exists solely to produce a measurement. | **Confirmed** |
| D-17 | Encouragement is a retrospective, additive record of completed Lane B items. Never a streak, counter, badge, or deadline, and never on Lane A. | **Confirmed** |

D-11 exists because a ranked list always looks intelligent, and Barbara works in evaluation design. The deletability of the prioritization layer is a product decision, not a technical one, and it should survive into whatever gets built.

D-15 is a latency measure rather than a count because promotion is the *save* gesture: under the failure mode described in F-03, a promotion count rises as the system stops working. Latency degrades in the correct direction, cannot be inflated by keeping more or keeping less, is readable after two or three items rather than after a month, and creates no recurring deadline — which matters because D-02 makes absence free, and a weekly pass/fail would quietly take that back.

D-16 is the durable guard. It is what should stop a later session from helpfully adding a "mark as read" control in order to make some number easier to compute. The test it encodes: a metric derived from a gesture Barbara would make anyway is safe; a metric requiring a gesture she would only make to feed the metric is the disease.

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
| A-05 | ~~Enterprise data management sources are vendor-dominated with a low signal rate and need different handling from the ML sources.~~ **Retired 6 Sep 2026 — the question was wrong.** The discovery pass found no enterprise data management sources at all (F-06), so there is nothing to characterise as vendor-dominated. | Claim made during analysis; the pass tested it and found no population. | Superseded by question 3, which now asks whether she wants the field covered at all. |
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
3. **Does enterprise data management belong in scope at all?** **Reframed by F-06.** The original question assumed she followed the field and asked why. She does not follow it: the pass found zero enterprise data management sources. So the real question is whether Section 1's three named fields describe what she wants to read or what she wishes she read. If the latter, the system has to seed sources she is not subscribed to, which is a different and larger job than filtering what arrives.
4. **How does Lane A arrive?** D-09 says it arrives rather than being fetched. The mechanism was not settled. Candidates discussed: a message to herself, a bookmarked destination, or a message linking to a destination. The argument for a message is that it borrows a habit she already has instead of asking her to form one.
5. **What is the Lane B cap, exactly?** "Seven or so" was as far as it got. The cap existing is the decision; the number is not settled.
6. **Does expiry survive contact with her habits?** A-01 is argued from category history rather than from her behavior. If she has a counterexample from her own life, that outranks anything cited here.
7. **What is the gesture called?** "Favorite" and "keep" were both used for the same action.
8. **How far does related content extend?** TED talks were the stated example. Whether it covers papers, conference talks, or other media was never scoped.

Added in v1.3, from the discovery pass:

9. **How big is one Lane A delivery?** The most consequential new question. Section 3.2 says size is uncontrolled. At 150–250 candidate items per week that produces a wall, and a wall is not skimmable. Either Lane A gets a hard size limit like Lane B, or the prioritisation layer becomes load-bearing rather than optional, or both. This decision interacts with A-02: a smaller cadence means a smaller batch.
10. **Which addresses count as sources?** F-05 found at least three delivery addresses in one mailbox, with the same publication arriving twice. Deduplication is required. Whether all three addresses are in scope is Barbara's call.
11. **Is "field-adjacent" defined by her subscriptions or by her intent?** F-06 found her actual reading interests cluster in AI/LLM/agents and software-product engineering, with a substantial non-field stream (military analysis, cooking, games, epidemiology) mixed into the same labels. D-12 already treats beginner content as noise; this asks the prior question of what counts as signal.

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

Questions 1 and 2 are closed. The order is now:

1. Resolve question 9, Lane A batch size. It is the largest open product decision and the one the discovery pass created. Everything about what Lane A feels like depends on it.
2. Resolve question 11, then question 3. Both define what counts as signal, and both change the source list rather than merely reordering it.
3. Put the remaining `Proposed` decisions to Barbara for explicit confirmation or rejection. **Two of seventeen decisions are currently unratified: D-08 and D-11.** D-11 matters more now than it did: A-07 holds, so a prioritisation layer will be built, and D-11 is the only thing standing between it and theater.
4. Take A-02, the cadence assumption, together with question 9. Barbara's rejection of a month-long evaluation window in the v1.2 discussion is evidence bearing on it, and cadence and batch size cannot sensibly be decided apart.
5. Resolve question 10, deduplication scope. Small, but it changes what a Source is.

Only then does architecture become a sensible next step.
