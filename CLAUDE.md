# CLAUDE.md

Read and follow `AGENTS.md`.

Read `docs/product-brief.md` before substantive product, planning, review, or implementation work.

This file is intentionally small. Shared project knowledge belongs in the repo, not in Claude-specific instructions.

---

## Claude-specific rules

### Verify before asserting

**`AGENTS.md` section 1 is the full rule set** — your own prior output is a hypothesis, effort estimates are claims about code, re-read before advising on what you just wrote, and never claim behaviour you have not observed. Those are cross-harness and are not repeated here. What follows is only the Claude-specific part.

For claims about the repository, use filesystem / Git tools appropriate to the claim.

Do not infer that a directory is absent because a file search, glob, or `git ls-files` did not show it. Empty directories are not tracked by Git and may be invisible to file-oriented searches.

For claims about available Claude Code / ECC capabilities, verify availability in the current session before naming them as usable.

### Use ECC selectively, and report on it

ECC is a toolbox, not a checklist.

Use a skill, agent, hook, or orchestration pattern only when it adds clear value to the current task.

Do not use ECC merely to demonstrate ECC.

**Report at every artifact hand-off.** Part of this project's purpose is learning which ECC components materially help. Whenever you deliver a working artifact or reach a natural stopping point, add a short section covering, for each ECC component that actually fired:

- what failure mode it exists to prevent,
- what it changed in this session, concretely,
- whether the benefit justified the friction — say plainly when it did not.

A few lines per component. This is an honest assessment, not a defence of the tooling.

### Keep outputs readable

Lead with **What matters now**.

Prefer compact bullets and short headings.

Do not use the section symbol (`§`) in user-facing prose.

Use product-brief IDs such as `D-04` or `A-02` when exact traceability helps.

Do not overwhelm the user with every observation when a smaller set determines the next decision.

### Preserve epistemic status

Do not convert `Proposed`, `Assumption`, or `Unresolved` items in the product brief into settled product requirements.

Narrative examples and candidate models do not override explicit status labels.

### Design and build without waiting for permission

**Changed 7 Sep 2026.** This rule previously read "do not design architecture or implement unless the user explicitly moves the project into that phase." That gate is removed. It was producing plans whose critical path was waiting, and it is the direct cause of the project stalling.

Follow `AGENTS.md` section 3: once Barbara has approved *what* a thing should do, design it and build the smallest usable version. Do not stop to ask whether you may start.

Two things this does **not** license:

- Inventing answers to unresolved product questions. Propose, label it a proposal, and keep moving on everything that does not depend on the answer.
- Building more than was asked for.

When asked for independent review, still critique the artifact before attempting to improve it.

### Persist only what matters

Important cross-session decisions should become repository artifacts.

Do not create documentation, memory, or orchestration layers just because they are available.
