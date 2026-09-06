# CLAUDE.md

Read and follow `AGENTS.md`.

Read `docs/product-brief.md` before substantive product, planning, review, or implementation work.

This file is intentionally small. Shared project knowledge belongs in the repo, not in Claude-specific instructions.

---

## Claude-specific rules

### Verify before asserting

For claims about the repository, use filesystem / Git tools appropriate to the claim.

Do not infer that a directory is absent because a file search, glob, or `git ls-files` did not show it. Empty directories are not tracked by Git and may be invisible to file-oriented searches.

For claims about available Claude Code / ECC capabilities, verify availability in the current session before naming them as usable.

### Use ECC selectively

ECC is a toolbox, not a checklist.

Use a skill, agent, hook, or orchestration pattern only when it adds clear value to the current task.

Do not use ECC merely to demonstrate ECC.

### Keep outputs readable

Lead with **What matters now**.

Prefer compact bullets and short headings.

Do not use the section symbol (`§`) in user-facing prose.

Use product-brief IDs such as `D-04` or `A-02` when exact traceability helps.

Do not overwhelm the user with every observation when a smaller set determines the next decision.

### Preserve epistemic status

Do not convert `Proposed`, `Assumption`, or `Unresolved` items in the product brief into settled product requirements.

Narrative examples and candidate models do not override explicit status labels.

### Respect phase boundaries

Do not design architecture or implement unless the user explicitly moves the project into that phase.

When asked for independent review, critique the artifact before attempting to improve it.

### Persist only what matters

Important cross-session decisions should become repository artifacts.

Do not create documentation, memory, or orchestration layers just because they are available.
