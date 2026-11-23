# Module Doc

Write a `CLAUDE.md` for one module (a folder of code). Claude Code loads it only when working in that folder, so it holds rules that matter there and nowhere else.

Use it when a module has rules the agent keeps breaking, or when the root `CLAUDE.md` is filling up with one module's detail. A small project doesn't need any.

## Steps

1. **Gather information** — Take what you can from the conversation and the code first. Ask only for what's missing, in a single message:
   - Module path (e.g. `src/noise/`)
   - What the module does and where it sits in the system, in one or two sentences
   - Rules that must not break in this module
   - Gotchas: traps that aren't obvious from the code
   - Common tasks, if any recur

2. **Check before writing** — Flag any of the following and ask whether to proceed or revise:
   - A rule that can't be checked against a diff ("keep it clean"). Ask for a specific version ("noise is added to training labels only").
   - Content the code already shows: function lists, signatures, field tables. Leave it out; it goes stale.
   - Design rationale ("we chose X because..."). That belongs in an ADR (`/decision`).
   - A rule that applies to the whole project. That belongs in the root `CLAUDE.md`.

3. **Write the file** — Write `CLAUDE.md` to the module path using the template below. Omit any section with nothing in it; don't leave placeholders.

4. **List it** — In the root `CLAUDE.md`, add a line under `**Module docs**` in Key Docs:
   ```
   - [Module name]: `[path/to/module/CLAUDE.md]`
   ```
   If the list still has its placeholder line, replace it. Don't change anything else in the root file.

5. **Confirm** — Tell the user the path created and whether the root list was updated. If they described choices between alternatives, run `/decision` for each.

---

## Template

```markdown
# [Module name] - [Project Name]

[One or two sentences: what this module does and where it sits in the system.]

## Must not break

- [A rule a diff can be checked against, e.g. "Noise is added to training labels only; test labels are never changed."]

## Gotchas

- **[Short title]**: [What happens and what to do instead.] (`[file:line]`)

## Common tasks

- **[Task]**: [Command or steps.]

---

**Last Updated**: [YYYY-MM-DD]
```

---

## Rules

- Keep it short. Most module docs are under 40 lines; past 80, check for content the code already shows.
- Rules must be falsifiable: "status is one of `idle`, `staged`, `live`", not "status should be valid".
- If modules react to each other's events, the reactions go in `SYNCHRONIZATIONS.md` (`/sync-flow`), not here.
