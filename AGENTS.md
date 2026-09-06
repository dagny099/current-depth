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

## 3. Respect the task boundary

If asked to inspect or summarize, do not plan.

If asked to plan, do not implement.

If asked to review, evaluate independently before proposing rewrites.

If asked to implement, follow the accepted artifacts and surface material deviations.

Do not make technical choices merely to make the repository look initialized.

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
