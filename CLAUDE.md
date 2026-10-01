# Agentic Coding Framework

A documentation template that people copy into a new project so their coding agent starts with goals, conventions and decision history. This file is for working on the framework itself; the template users copy is `templates/CLAUDE.md`.

**Stack**: Markdown only. No build, no tests, no package.

---

## Layout

- `templates/`: the files users copy into their project root (`cp -r templates/. your-project/`). Everything here ships to every project.
- `.claude/commands/`: slash commands. Users copy the whole folder, and they also work when you're in this repo.
- `examples/`: worked concept `CLAUDE.md` files and an example `SYNCHRONIZATIONS.md`.
- `docs/ADVANCED_FEATURES.md`: optional patterns (sections 7–8: enforcing conventions in code, hooks).
- `README.md`, `GETTING_STARTED.md`, `CONTRIBUTING.md`: framework docs for humans.
- `DECISIONS.md`: this repo's own ADRs, about how the framework is designed. Not a template.

---

## Conventions

**Templates (`templates/`, `.claude/commands/`, `examples/`)**
- Nothing project-specific or framework-internal goes in `templates/`. It is copied verbatim into every new project.
- Placeholders use `[Square brackets]`. No real-looking dates, versions or release history; a dated example goes inside an HTML comment or is marked "e.g.".
- `templates/CLAUDE.md` loads into every session of every project that uses it. Every line added there must be worth that cost; longer guidance goes in `GETTING_STARTED.md` or `docs/`.
- Links between template files are relative to `templates/` (they sit side by side in the user's project). Links from a template out to framework docs use the full GitHub URL, since those files are not copied.

**Keeping things in sync**
- Adding, renaming or removing a file in `templates/` → update the comment listing it in `GETTING_STARTED.md` step 1 and the tree in `README.md` "Framework Overview".
- Adding or removing a command → update the command table in `README.md` and the maintenance table in `GETTING_STARTED.md`.
- Choosing between alternatives about the framework's design → append an ADR to the root `DECISIONS.md` (`/decision` works here too).

**Writing**
- Plain, specific sentences. State rules as checkable statements.
- No emoji in new text.

---

## Definition of Done

1. Relative Markdown links resolve (ignoring links inside code spans and fences, and the deliberate `(link)` placeholders in `templates/PROJECT_PLAN.md`).
2. `grep -rn "your-username\|20[0-9][0-9]-" templates` finds nothing (real-looking dates or placeholder URLs leaking into templates). Dates inside `.claude/commands/` format examples are fine.
3. If you changed copy instructions, `templates/`, `examples/` or `.claude/commands/`: in an empty scratch folder (create nothing by hand), run the copy commands exactly as `README.md` and `GETTING_STARTED.md` give them. Every command succeeds, and the link check from step 1 passes on the copied project, not just this repo.
4. If you changed a code snippet in `docs/ADVANCED_FEATURES.md`: run it.
5. Say explicitly what you did not verify (for commands, usually: not run in a real Claude Code session).

---

**Last Updated**: 2026-10-01
