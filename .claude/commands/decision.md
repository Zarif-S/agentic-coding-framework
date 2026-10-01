# Decision

Record a decision as an ADR in `DECISIONS.md`: what we chose, what we rejected, and why. Use this whenever a choice between real alternatives has been made.

## Steps

1. **Find DECISIONS.md** — Look for it at the project root. If it doesn't exist, tell the user and offer to create it from the framework template before continuing.

2. **Read existing entries** — Scan the file to:
   - Determine the next ADR number (if ADR-006 is the last entry, the new one is ADR-007)
   - Check whether an existing Accepted ADR covers the same question. If so, this new decision probably supersedes it; confirm with the user

3. **Gather information** — Extract as much as possible from the current conversation first. Decisions usually come up mid-task, and the context is already there. Only ask for what's missing, in a single message:
   - **Context**: what situation or constraint forced a choice?
   - **Options considered**: at least two, each with its main pro and con
   - **Decision**: which option, in one or two sentences
   - **Consequences**: what this makes easier or harder; what would make us revisit it

4. **Validate before writing** — Flag any of the following and ask whether to proceed or revise:
   - Only one option listed. If there was no real alternative, this probably isn't an ADR; suggest a Gotcha in CLAUDE.md or nothing at all
   - Consequences are all positive. Every real decision has a cost; ask what it is
   - The decision is about agent behaviour or a recurring mistake rather than a design choice. That belongs in LESSONS_LEARNED.md and the Conventions section of CLAUDE.md instead

5. **Append the entry** — Add it at the end of the `## Decisions` section using the exact format below. Remove the `[Add ADR entries here...]` placeholder line if it's still there. If this supersedes an earlier ADR, change only that ADR's `**Status**` to `Superseded by ADR-NNN`; do not edit its other content.

6. **Link from other docs** — If the decision relates to a PROJECT_PLAN.md item, ROADMAP.md initiative, or concept CLAUDE.md, suggest a one-line link ("see ADR-NNN"). Ask before editing those files.

7. **Confirm** — Tell the user the ADR ID assigned, any ADR it supersedes, and any links added.

---

## Entry Format

```markdown
### ADR-NNN: [Short title, phrased as the decision]

**Date**: YYYY-MM-DD · **Status**: Accepted

**Context**: [The situation and constraints at the time.]

**Options considered**:
- **[Option A]**: [main pro / main con]
- **[Option B]**: [main pro / main con]

**Decision**: [What we chose.]

**Consequences**: [What gets easier, what gets harder, when we'd revisit.]

---
```

---

## Rules

- Never edit the substance of an existing ADR. Only the Status line of a superseded ADR may change
- Never renumber ADRs; IDs are stable references
- One decision per ADR. Split bundled decisions into separate entries
- Use today's date, not the date the decision might have been made earlier
- Do not invent options the user didn't consider. If the conversation only shows one option, ask what else was on the table
- Keep entries short: five to fifteen lines
