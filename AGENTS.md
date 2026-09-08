# AGENTS.md

## Purpose

This is a **small cross-harness operating contract**, not a product specification.

Keep it light.

Product facts, decisions, assumptions, and unresolved questions belong in `docs/product-brief.md`. Do not duplicate them here.

If this file conflicts with the product brief, the product brief wins.

---

## 1. Establish ground truth before making claims

### Repository state

Before stating that a file or directory exists, is missing, is tracked, or is untracked:

- verify it with an appropriate filesystem or Git command;
- distinguish **filesystem state** from **Git-tracked state**;
- do not infer directory existence from file search results alone.

Important: **Git does not track empty directories.** File-oriented search tools may also omit them.

If you did not verify a repo-state claim, say `not verified`.

### Product state

When using `docs/product-brief.md`, preserve its epistemic labels:

- `Confirmed`
- `Proposed`
- `Assumption`
- `Unresolved`

Never promote a `Proposed` item or an assumption into a settled requirement because it appears in narrative prose, a table, a candidate entity list, or another agent's summary.

When two parts of the brief appear inconsistent, use the decision / assumption status rules in the brief and surface the inconsistency.

### Tool and capability state

Do not claim that a connector, skill, agent, hook, or other capability is available unless you actually verified it in the current harness/session.

### These bind what you say, not what you do

**Read this before the four rules below.** They govern **assertions**, not actions. Nothing here licenses waiting, gathering more evidence before starting, or adding a verification step to the front of a build — section 3 forbids that and outranks this section. Build first; the rules apply the moment you make a claim *about* what you built.

The cost of following them is a sentence — "not verified", or a shape without a number. It is never a delay.

### Your own prior output is a hypothesis

A session summary, a handoff, a file you wrote an hour ago, a number you yourself put in a commit message: none of it is established fact. Re-derived confidence is the most common way a wrong claim survives.

Scope this, or it becomes ritual. Verify before repeating **any claim that could change a decision Barbara makes.** For claims that could not, write `not verified` inline and move on — do not stop to check them, and do not silently drop them either.

### Effort and size estimates are claims about code

"Ten lines", "two minutes", "just hygiene", "trivial", "a one-line fix": each is a factual claim about a file. Do not state one unless you have opened the file in this session.

If you have not, describe the **shape** without the number — "a change confined to the render path", "one constant and its two callers". A shape you can defend beats a number you guessed.

### Re-read before advising on what you just wrote

Before giving advice, a recommendation, or a summary that touches a file you edited **this session**, read the current state of that file back.

Recently-written text is the material most likely to be misremembered, because it feels known. This is how a rule gets written and then contradicted an hour later in the same document.

### Never claim behaviour you have not observed

Reading the code that should produce a behaviour is **not** observing the behaviour. Publishing a page that says it syncs is not evidence that it syncs.

Before writing that something works — in prose, in a commit message, or in the product's own copy — either observe it, or say precisely what was implemented and what remains unverified. "The store now holds the document" requires a read. "I changed how writes are queued" does not.

When a fix is a hypothesis, say so and name what would confirm it. A confident wrong diagnosis costs more than an admitted uncertain one, because it ends the investigation.

---

## 2. Keep outputs easy to read

The user is making decisions while reading. Optimize for signal.

Default response shape:

1. **What matters now** — 1–4 bullets
2. **What I verified** — only when factual verification matters
3. **Decision / recommendation** — clearly separated from evidence
4. **Next action** — only the smallest useful next step

Additional detail can follow when it materially helps.

### Readability rules

- Lead with the important conclusion, not a transcript of your process.
- Prefer short headings and compact bullets.
- Avoid long inventories unless requested.
- Do not use the section symbol (`§`) in user-facing prose.
- When referring to the product brief, prefer decision IDs such as `D-04`, assumption IDs such as `A-02`, or plain-language heading names.
- Do not bury uncertainty in dense prose.
- Mark material uncertainty explicitly.
- Use tables only when they make comparison easier.

---

## 3. Build in loops, not phases

**Set 7 Sep 2026 by Barbara. This overrides any earlier sequencing language anywhere in this repo.**

The working cycle is:

> understand the requirement → get her approval on the requirement → design → build the smallest usable version → put it in front of her → learn → iterate.

Rules that follow from it:

- **Approval is needed on requirements, not on permission to work.** Once she has agreed what a thing should do, design and build it. Do not wait for a separate authorisation to begin.
- **Do not gate building on evidence collection.** Evidence accrues from her using the thing. A rough version she can use this week beats a clean version she can use next month.
- **Never propose a plan whose first milestone is weeks of data collection.** If a plan's critical path is "wait and observe", the plan is wrong.
- **Fail fast in public.** Ship it, watch it break, fix it. A wrong version in her hands is more informative than a correct document.
- **Clean experimental design is a nice-to-have, not a blocker.** Prefer a usable result with a caveat over a pristine result that arrives too late to matter.

Still true, and not softened by the above:

- If asked to review, evaluate independently before proposing rewrites.
- If asked a question, answer it — do not convert it into a project.
- Do not make technical choices merely to make the repository look initialized.

### Evaluation rules decide what ships. They do not gate work.

`D-11` (a ranking must beat newest-first or be deleted) and `D-15` (median keep-to-done of 14 days or less) are **decision rules about what survives**, not permission gates on building. Build the thing; let the rule decide later whether it stays. Nothing in this repo may be described as "blocked" on an evaluation that has not run yet.

---

## 4. Keep durable knowledge in the repo

Conversation history is not authoritative project state.

When a decision or artifact needs to survive another session or harness, write it to an appropriate repository file.

Typical locations:

- `docs/product-brief.md` — product truth
- `docs/plans/` — plans
- `docs/reviews/` — independent reviews and adjudications
- `docs/evals/` — evaluation definitions and results

Do not create new documentation layers without a concrete need.

---

## 5. Preserve independence in cross-harness experiments

When comparing Claude Code, Codex, Cursor, models, or workflows:

- start from the same frozen input when possible;
- do not expose one agent's reasoning or output to another unless the experimental design calls for it;
- record which variables changed;
- do not claim a model effect when the harness also changed.

A new model is a challenger, not automatically the new default.

---

## 6. Complexity must earn its keep

Use agents, skills, hooks, orchestration, MCPs, frameworks, dependencies, and abstractions only when they materially improve the task.

Prefer the smallest coherent next step.

If the same result can be achieved with a simpler, more inspectable workflow, prefer that.

---

## Before saying a task is complete

Check:

- Did I verify factual repo-state claims?
- Did I preserve `Confirmed` / `Proposed` / `Assumption` / `Unresolved` status?
- Did I stay inside the requested task boundary?
- Did I make the output easy to scan?
- Did I persist anything another session genuinely needs?
- Did I avoid unnecessary complexity?
