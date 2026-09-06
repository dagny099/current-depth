# Reading Digest — Product Brief

**Version** 1.2 · 6 Sep 2026
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

One mailbox was inventoried (`barbs@geocue.me`, 5 Sep 2026). Findings, scoped honestly:

| ID | Finding | Status |
|---|---|---|
| F-01 | That account carries essentially no DS/ML editorial newsletters. Fourteen named publications searched across inbox, archive, spam and trash; one hit, a false positive. | **True but superseded.** It was the wrong mailbox. |
| F-02 | 933 unread of 1,054 (88%). Zero user labels, zero filters. ~6.7 messages/day. One commercial sender alone sent 18 messages in 30 days, exceeding every field-adjacent sender combined. | **Holds.** Corroborates the described deterrent effect. Does not establish causation. |
| F-03 | Unread accumulation is the documented dominant failure mode of read-it-later tools. | **Holds**, moderate confidence (see 1.3). |
| F-04 | Arrival rate and composition at `dagny099@gmail.com` — the account that actually carries the subscriptions — are unknown. | **Open.** Blocking. |

F-04 is the single most consequential gap in this brief. Volume determines whether prioritisation is worth building at all.

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
| Size | Whatever arrived | Hard cap (7 or so) |
| Actions | Keep, less like this | Notes, done |
| Keep does | Promotes into Lane B | n/a |

Terminology note: "favorite" and "keep" refer to the same gesture. This brief now writes it as **keep** throughout for consistency, but the name is still unresolved (question 7) and using it here does not settle it.

The Actions row changed in v1.2. Lane A previously had one action; it now has two, per D-14.

### 3.2 Lane A — Current awareness

Current working behavior:

- Arrives on a weekly cadence. Barbara does not fetch it. A destination she must remember to visit is a destination she will stop visiting.
- Items expire approximately ten days after arrival, silently, with no action from her. The ten days give roughly one week of overlap so nothing vanishes between one delivery and the next.
- Size is uncontrolled: whatever arrived, arrived.
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
| A-05 | Enterprise data management sources are vendor-dominated with a low signal rate and need different handling from the ML sources. | Claim made during analysis. Not checked against her actual subscriptions. | Resolves during the F-04 discovery pass. |
| A-06 | The measured clutter in the other mailbox represents the deterrent effect she described. | Corroboration only. Causation not established. | Would require observing her behavior, not her mailbox. Probably not worth testing. |
| A-07 | There is enough arriving to justify a prioritization layer. | Unknown. F-04 is open. | The discovery pass, then one week of observed volume. |
| A-08 | She will mark `done` on Lane B reliably enough for D-15's latency to mean anything. | Inference, not observation. Plenty of people finish the article and never tap the button. | After one month, compare the done count against her own recollection of what she actually finished. A large gap invalidates D-15 rather than her reading. |
| A-09 | Taking items off Lane A via "less like this" will not turn Lane A into a surface she clears. | Judgment. She chose hiding over signal-only in v1.2 with the clearing risk stated. | Hide-to-keep ratio per delivery cycle. If hides run well ahead of keeps, Lane A has become a list to clear, and the correct response is a narrower digest, not a better hide control. |

A-07 is the one that could collapse a large part of this design. If arrival volume turns out to be low, chronological order is already correct and the prioritisation layer should never be built.

---

## 7. Unresolved product questions

Ordered by how much they block.

1. **What is actually arriving?** Rate and composition at `dagny099@gmail.com`. Blocks everything downstream. Access is the constraint: the mailbox was not reachable from the working session, and the fallback is Barbara listing her subscriptions by hand.
2. **What outcome would she notice?** **Resolved in v1.2 — see D-15, D-16, D-17.** Question text kept so the record of what was open survives. The answer landed on a latency criterion (median keep to done, 14 days) rather than a count, because a count of promotions rises in the failure mode; on a rule governing which gestures may be measured at all; and on encouragement being a growing record of finished items rather than a streak.
3. **Is enterprise data management job-driven or interest-driven?** Different source ecosystems, different skepticism, different subscription list. Changes what gets followed, not just how it is ranked.
4. **How does Lane A arrive?** D-09 says it arrives rather than being fetched. The mechanism was not settled. Candidates discussed: a message to herself, a bookmarked destination, or a message linking to a destination. The argument for a message is that it borrows a habit she already has instead of asking her to form one.
5. **What is the Lane B cap, exactly?** "Seven or so" was as far as it got. The cap existing is the decision; the number is not settled.
6. **Does expiry survive contact with her habits?** A-01 is argued from category history rather than from her behavior. If she has a counterexample from her own life, that outranks anything cited here.
7. **What is the gesture called?** "Favorite" and "keep" were both used for the same action.
8. **How far does related content extend?** TED talks were the stated example. Whether it covers papers, conference talks, or other media was never scoped.

---

## 8. Candidate concepts and entities

This is a **vocabulary sketch, not a settled domain model**. It exists to make product discussion concrete without choosing storage, schema, field types, or architecture.

Some concepts below depend on `Proposed` decisions or assumptions. Their appearance here does **not** make those decisions confirmed.

| Concept | What it represents | Status / dependency |
|---|---|---|
| **Source** | A publication Barbara may choose to follow. | Conceptually useful; exact source set is blocked by F-04. |
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

1. Resolve unresolved question 1: what is actually arriving at `dagny099@gmail.com`? Nothing downstream is decidable without it. State the arrival rate in two units — messages per week, and candidate items per week — because they differ by roughly an order of magnitude and A-07 depends on which one is meant.
2. Resolve unresolved question 3 with Barbara directly. Cheap, and it changes scope. Question 2 is closed as of v1.2.
3. Put the remaining `Proposed` decisions to Barbara for explicit confirmation or rejection. **Two of seventeen decisions are currently unratified: D-08 and D-11.**
4. Take A-02, the cadence assumption. Barbara's rejection of a month-long evaluation window in the v1.2 discussion is evidence bearing on it.

Only then does architecture become a sensible next step.
