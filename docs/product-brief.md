# Reading Digest — Product Brief

**Version** 1.0 · 5 Sep 2026
**Owner** Barbara (single user; this is a personal system, not a product)
**Status** Pre-architecture. Requirements settled enough to hand off; nothing built.

---

## 0. How to read this brief

You have no access to the conversation that produced this. Everything you need is here.

Two conventions matter:

**Every decision below is tagged with its firmness.** `Confirmed` means Barbara explicitly chose it. `Proposed` means it was put to her, went uncontested, and is written into the requirements, but she never affirmatively ratified it. Treat `Proposed` items as revisable on contact with her; do not treat them as settled just because they appear here.

**Assumptions are separated from decisions on purpose.** Several load-bearing parts of this design rest on inference rather than on Barbara's stated behavior. Those are listed in §6 with their basis. If you find yourself building something that depends on an assumption, surface it rather than hardening it.

### Out of scope for the next work

Explicitly requested by Barbara, and binding on you:

- Do not design the technical architecture. No storage design, no pipeline topology, no tool or vendor selection.
- Do not implement anything.
- Do not fill gaps with new product ideas. Where this brief says a question is unresolved, it is unresolved, and inventing an answer destroys the record of what was actually decided.

Companion documents (same project, published separately): a requirements document with numbered requirements `R-01`–`R-10`, goals `G-01`–`G-03`, constraints `C-01`–`C-03`, and evidence findings `F-01`–`F-04`; and a staged build plan. This brief supersedes neither and duplicates what you need.

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

Written from Barbara's side of the screen.

Once a week, something arrives carrying a handful of things worth knowing about in her fields. She reads it or she does not. If she does not, nothing happens: no counter climbs, no badge appears, nothing waits for her. The items age out on their own within days and leave no residue. Ignoring it for three weeks costs nothing and leaves the system in a good state.

When something in that weekly arrival is worth more than a skim, she makes **one gesture**. That is the only action available. The item moves onto a small shelf that does not expire and does not grow past its cap. The shelf is where she goes when she has an hour rather than five minutes, and it is the only place the system ever offers her additional material — a related talk, a related paper — because offering more things to read in the weekly stream would be the disease, not the treatment.

The shelf being capped is the mechanism, not a limitation. Adding a new item when it is full requires removing one, which forces a choice she would otherwise defer indefinitely.

Nothing in this experience involves dismissing, archiving, marking read, or clearing a list. Those actions are absent by design. Disappearance is the default state, and attention is the only thing that overrides it.

---

## 3. Lane A and Lane B

### 3.1 The table

Reproduced from the working session, unchanged in meaning:

| | Lane A — Current | Lane B — Study |
|---|---|---|
| Cadence | Weekly batch | Added by hand, no schedule |
| Lifetime | Items expire ~10 days, silently | No expiry |
| Size | Whatever arrived | Hard cap (7 or so) |
| Actions | Favorite only | Notes, done |
| Favorite does | Promotes into Lane B | n/a |

Terminology note: "favorite" and "keep" refer to the same single gesture. Pick one name and use it consistently; the name was never settled.

### 3.2 Lane A — Current awareness

Operating rules:

- Arrives on a weekly cadence. Barbara does not fetch it. A destination she must remember to visit is a destination she will stop visiting.
- Items expire approximately ten days after arrival, silently, with no action from her. The ten days give roughly one week of overlap so nothing vanishes between one delivery and the next.
- Size is uncontrolled: whatever arrived, arrived.
- Exactly one action exists, and it means "this one matters."
- There is no dismiss, no mark-read, no archive. Removal is what happens when she does nothing.
- No related or suggested material appears here, ever.
- What expires unkept is recorded. That record is the evidence base for testing assumption A-01 (§6).

### 3.3 Lane B — Deliberate study

Operating rules:

- Populated only by the Lane A gesture, or by hand.
- No cadence. Nothing arrives here on a schedule.
- No expiry. Items persist until she removes them.
- Hard cap on size. Adding past the cap requires removing something first.
- Actions available: notes, and marking done.
- This is the only surface where related material is offered, and only per item, on demand.

### 3.4 The relationship between lanes

One-directional. Lane A feeds Lane B through the single gesture. Nothing flows back. Lane A's job is to be forgettable; Lane B's job is to be persistent; and the gesture is the only bridge.

---

## 4. Decisions already made

| # | Decision | Firmness |
|---|---|---|
| D-01 | Two separated surfaces, current-awareness and deliberate study, rather than one combined feed. | **Confirmed** |
| D-02 | Items on Lane A expire on their own. No dismiss action exists. | **Confirmed** |
| D-03 | Newsletter subscriptions live at `dagny099@gmail.com`, not the account already inventoried. | **Confirmed** |
| D-04 | That mailbox gets one discovery pass to learn what she already subscribed to. Email is a source of inspiration for the source list, not a runtime input to the system. | **Confirmed** |
| D-05 | Related content stays in scope. | **Confirmed** (she asked for it, naming TED talks as the example) |
| D-06 | Related content is confined to Lane B and never appears on Lane A. | **Proposed** |
| D-07 | The single Lane A gesture promotes the item into Lane B. | **Proposed** |
| D-08 | Lane B is capped. Adding past the cap requires removing. | **Proposed** |
| D-09 | Lane A arrives rather than waiting to be visited. | **Proposed** |
| D-10 | Whatever decides relevance must be inspectable and editable by her: she can see what the system believes she cares about, see why an item surfaced, and change both. | **Proposed** |
| D-11 | Any prioritisation layer must beat a chronological baseline on a hand-labeled set, with the threshold written down in advance, or be removed. Removing it counts as a good outcome. | **Proposed** |
| D-12 | Content pitched at beginners in retrieval, evaluation and knowledge graphs is treated as noise. | **Proposed** |
| D-13 | Requirements and problem statement are maintained separately from any solutioning. | **Confirmed** |

D-11 exists because a ranked list always looks intelligent, and Barbara works in evaluation design. The deletability of the prioritisation layer is a product decision, not a technical one, and it should survive into whatever gets built.

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
| Read/unread state, archive, dismiss | Designed out deliberately. Their absence is the differentiating decision, not an omission to be helpfully filled in later. |
| Runtime access to her mailbox | Email appears once, for source discovery. The running system does not read her mail. |

---

## 6. Assumptions

Each is a place where the design rests on inference. None has been validated against Barbara's behavior.

| # | Assumption | Basis | How it could be tested |
|---|---|---|---|
| A-01 | Expiry suits her. Queues she keeps would rot. | Category history (F-03), not her data. | Record what expires unkept for a month. If she repeatedly wishes she still had something, the assumption is wrong. |
| A-02 | Weekly is the right Lane A cadence. | Never discussed. Assumed. | Ask. Cheap to change before anything exists. |
| A-03 | Ten days is the right expiry window. | Derived from A-02, to give one week of overlap. | Falls with A-02. |
| A-04 | She is past introductory material in retrieval, evaluation and knowledge graphs. | Her stated background. | High confidence. |
| A-05 | Enterprise data management sources are vendor-dominated with a low signal rate and need different handling from the ML sources. | Claim made during analysis. Not checked against her actual subscriptions. | Resolves during the §1.4 F-04 discovery pass. |
| A-06 | The measured clutter in the other mailbox represents the deterrent effect she described. | Corroboration only. Causation not established. | Would require observing her behavior, not her mailbox. Probably not worth testing. |
| A-07 | There is enough arriving to justify a prioritisation layer. | Unknown. F-04 is open. | The discovery pass, then one week of observed volume. |

A-07 is the one that could collapse a large part of this design. If arrival volume turns out to be low, chronological order is already correct and the prioritisation layer should never be built.

---

## 7. Unresolved product questions

Ordered by how much they block.

1. **What is actually arriving?** Rate and composition at `dagny099@gmail.com`. Blocks everything downstream. Access is the constraint: the mailbox was not reachable from the working session, and the fallback is Barbara listing her subscriptions by hand.
2. **What outcome would she notice?** Goal G-01 is "read more" and has no measurable form. Two articles a week finished? One thing a month that changes how she works? Without a criterion there is no way to distinguish a working system from a pleasant-looking one. This is the weakest part of the requirements.
3. **Is enterprise data management job-driven or interest-driven?** Different source ecosystems, different skepticism, different subscription list. Changes what gets followed, not just how it is ranked.
4. **How does Lane A arrive?** D-09 says it arrives rather than being fetched. The mechanism was not settled. Candidates discussed: a message to herself, a bookmarked destination, or a message linking to a destination. The argument for a message is that it borrows a habit she already has instead of asking her to form one.
5. **What is the Lane B cap, exactly?** "Seven or so" was as far as it got. The cap existing is the decision; the number is not settled.
6. **Does expiry survive contact with her habits?** A-01 is argued from category history rather than from her behavior. If she has a counterexample from her own life, that outranks anything cited here.
7. **What is the gesture called?** "Favorite" and "keep" were both used for the same action.
8. **How far does related content extend?** TED talks were the stated example. Whether it covers papers, conference talks, or other media was never scoped.

---

## 8. Likely data and entities

Conceptual domain model. No storage, no schema, no field types — those are architecture and are out of scope for now.

| Entity | What it represents | Notes |
|---|---|---|
| **Source** | A publication Barbara chose to follow. | Her keep-or-drop on each source is hers to make. No amount of downstream cleverness recovers from a bad source set. |
| **Item** | One piece of content from a Source. | The atom of both lanes. |
| **Lane A Placement** | An Item present in the current stream, carrying an arrival time and an expiry time. | Expiry is a property of the placement, not of the Item. |
| **Keep** | The single gesture. The event that promotes an Item from Lane A to Lane B. | Worth modeling as an event rather than a flag: it is also the strongest available signal of what she actually values. |
| **Shelf Entry** | An Item on Lane B, with notes and a done state. | No expiry. Subject to the cap. |
| **Interest Profile** | The statement of what she cares about, readable and editable by her. | D-10 requires that she can see and change this. It is a first-class object, not a hidden configuration. |
| **Relevance Judgment** | A score plus a human-readable reason, attached to an Item. | The reason is the interface through which she corrects the profile. Without it the filter drifts until she stops trusting it. |
| **Expiry Record** | What left Lane A unkept. | Retained deliberately as the evidence base for A-01. |
| **Related Suggestion** | A piece of material offered against a Shelf Entry. | Lane B only. Never attached to a Lane A Placement. |

Two relationships carry design weight:

- **Keep is the only path from Lane A to Lane B.** One-directional.
- **Related Suggestion attaches only to Shelf Entry.** If it can attach to a Lane A Placement, D-06 has been violated.

---

## 9. Known risks

Carried forward because they should inform product decisions, not just engineering ones.

- **It becomes a fourth place not to read.** Three surfaces already go unread. This is the default outcome for a project like this. The expiry design and the arrives-not-fetched decision are the mitigations.
- **The prioritisation layer is theater.** Plausible reasons attached to arbitrary ordering are indistinguishable from real relevance by inspection. D-11 exists for this.
- **Building it replaces reading.** The sharpest risk and specific to Barbara, who enjoys building. The project can succeed completely and still fail G-01. Any plan that puts a long build before a first working delivery is making this risk worse.

---

## 10. What a receiving agent should do first

Not architecture. In order:

1. Get the answer to §7 question 1. Nothing downstream is decidable without it.
2. Get answers to §7 questions 2 and 3 from Barbara directly. Both are cheap and both change scope.
3. Convert the `Proposed` decisions in §4 into `Confirmed` or `Rejected` by putting them to her. Six of thirteen decisions are currently unratified.

Only then does architecture become a sensible next step.
