# Plan Feature

Turn a feature description into a concrete documentation plan: a PROJECT_PLAN.md entry, plus a triage of every other doc that needs updating.

## Steps

1. **Understand the feature** — If the user has described the feature in natural language, use that. Otherwise ask in a single message:
   - What does the feature do? (user-facing description)
   - Which modules does it touch or add?
   - Is this new functionality, a change to existing behavior, or a fix?
   - Does it have any known dependencies or blockers?
   - Did planning it involve choosing between alternatives (approach, library, data format, where something lives)? If so, what were the options?

2. **Read project state** — Before generating anything, read:
   - `PROJECT_PLAN.md` — understand current focus, active Now/Next/Later items, and active blockers
   - `SYNCHRONIZATIONS.md`, if it exists: check whether the feature adds a reaction between modules
   - Root `CLAUDE.md`: "The system" section, and which module CLAUDE.md files exist (the `**Module docs**` list)
   - `ROADMAP.md`: identify which strategic initiative or milestone this feature belongs to
   - `DECISIONS.md`: check whether an existing ADR already covers a choice this feature depends on, or whether the feature contradicts one

   If any of these files don't exist, note which ones are missing but continue with what's available.

3. **Classify the feature** — Determine where it belongs in PROJECT_PLAN.md:
   - **Now**: user says it's actively being worked on, or it unblocks something currently in Now
   - **Next**: user intends to start it soon, or it depends on something in Now
   - **Later**: exploratory, speculative, or has no clear start date

4. **Triage doc updates** — For each document below, decide: `needs update`, `no change needed`, or `new file required`. Show the triage as a table before writing anything.

   | Document | Decision | Reason |
   |----------|----------|--------|
   | `PROJECT_PLAN.md` | needs update | Add feature to Now/Next/Later |
   | Root `CLAUDE.md` "The system" | needs update / no change | Does the flow or a must-not-break rule change? |
   | `[module]/CLAUDE.md` | needs update / no change | New must-not-break rule or gotcha? |
   | `SYNCHRONIZATIONS.md` (only if it exists) | needs update / no change | New reaction between modules? |
   | `ROADMAP.md` | needs update / no change | New initiative or milestone? |
   | `DECISIONS.md` | needs update / no change | Was a choice made between alternatives? Does it supersede an existing ADR? |
   | `CHANGELOG.md` | no change yet | Updated after implementation, not during planning |
   | `[new module]/CLAUDE.md` | new file required / not needed | New module with rules of its own? Most don't need one |

   Ask the user to confirm the triage before proceeding. If they want to adjust which docs get touched, revise and re-confirm.

5. **Write PROJECT_PLAN.md entry** — Append or insert the new item into the appropriate section (Now / Next / Later). Use this format:

   ```markdown
   **[N]. [Feature Name]**
   - **What**: [One sentence description of what this builds]
   - **Why**: [The user-facing or technical reason it's needed. If a choice was involved, link the ADR: "see ADR-NNN"]
   - **Who**: [Assignee or TBD]
   - **Status**: [Not started / In progress / Blocked]
   - **Depends on**: [Prerequisite features or decisions, if any]
   - **Tracking**: [Issue/ticket link, or "TBD"]
   ```

   Renumber existing items in the section if needed to maintain sequential numbering. Do not modify items in other sections.

6. **Apply remaining doc updates** — For each document marked `needs update` in the triage (except PROJECT_PLAN.md, already done):
   - If "The system" or a module CLAUDE.md needs a new rule or gotcha: add it. If a new module needs its own doc, suggest `/module-doc`.
   - If SYNCHRONIZATIONS.md needs a new entry: suggest running `/sync-flow` to add it properly, rather than writing it manually here.
   - If ROADMAP.md needs an initiative update: add the feature under the current quarter's Key Initiatives or flag it as a new initiative if it doesn't fit any existing one.
   - If DECISIONS.md needs an entry: write the ADR using the `/decision` format (next ADR number, options considered, decision, consequences), then link it from the PROJECT_PLAN.md entry's **Why** line. If the decision supersedes an existing ADR, update only that ADR's status line.

7. **Confirm** — Output a short summary:
   - Files updated and what changed in each
   - Any files that need follow-up (e.g. "Run `/module-doc` for the new module", "Run `/sync-flow` to add the new reaction")

---

## Rules

- Never add a feature to Now if PROJECT_PLAN.md already has 3+ active Now items — flag this and ask the user if something should move to Next first
- Never touch CHANGELOG.md during planning — it's updated after implementation, not before
- Never write decision rationale into PROJECT_PLAN.md or ROADMAP.md; it goes in an ADR, and those docs link to it
- If the feature contradicts an Accepted ADR, flag this before writing anything and ask whether the ADR should be superseded
- If SYNCHRONIZATIONS.md exists and the feature adds a reaction between modules, mark it `needs update` and direct the user to `/sync-flow`. Don't create SYNCHRONIZATIONS.md for a project whose steps run in order
- Do not invent tracking links — use "TBD" when none are provided
- Keep the PROJECT_PLAN.md entry concise; this is a planning artifact, not a spec.
- Strategic alignment in the entry ("Supports Q2 initiative: X") is optional but encouraged when the roadmap connection is clear
