# Doc Health

Scan all documentation files in the project for structural issues (broken links, stale dates, missing required sections, leftover placeholders, and orphaned files) and produce a prioritized fix list.

## Steps

1. **Discover all docs** — Find every Markdown file in the project:
   - Run a glob for `**/*.md` from the project root
   - Exclude: `node_modules/`, `.venv/`, `dist/`, `build/`, vendor directories
   - Group by type: root docs (`CLAUDE.md`, `ROADMAP.md`, `PROJECT_PLAN.md`, `CHANGELOG.md`, `SYNCHRONIZATIONS.md`, `DECISIONS.md`, `LESSONS_LEARNED.md`), concept CLAUDE.md files (any `CLAUDE.md` in a subdirectory), and other docs

2. **Run checks** — For each file, run all checks below. Collect every issue with its file path, line number (if applicable), severity, and a one-line description.

3. **Report** — Output a single prioritized report (Critical → Warning → Info), then ask: "Want me to fix any of these automatically?"

4. **Fix on request** — If the user says yes (to all or specific items), apply fixes. For issues that require judgment (e.g. rewriting a stale date, adding missing content), show the proposed change and confirm before writing.

---

## Checks

### Link checks (all docs)

**[CRITICAL] Broken relative link**
- Parse all `[text](path)` links that point to local files (skip `http(s)://` and pure `#anchor` links)
- Skip links inside fenced code blocks and HTML comments
- Resolve each path relative to the file's location
- Flag any that point to a file that doesn't exist

**[WARNING] Missing isolation rule**
- Every concept CLAUDE.md (any CLAUDE.md not at the project root) must contain the isolation rule blockquote:
  `> **Isolation rule**: This file describes only what this concept owns...`
- Flag concept files where this line is absent

---

### Date checks (all docs)

**[WARNING] Stale Last Updated date**
- Find lines matching `**Last Updated**: YYYY-MM-DD`
- Flag any date older than 90 days from today
- For PROJECT_PLAN.md specifically: flag if older than 30 days (it's a living document)

**[WARNING] Missing Last Updated line**
- Flag any doc that has no `**Last Updated**:` line at all

---

### Required section checks

**[CRITICAL] Root CLAUDE.md missing Key Docs section**
- The root CLAUDE.md must contain a `## Key Docs` section listing the root docs and a `**Concepts**:` list
- Flag if absent

**[WARNING] Root CLAUDE.md missing Conventions or Definition of Done**
- The root CLAUDE.md must contain `## Conventions` and `## Definition of Done` sections
- Flag whichever is absent

**[WARNING] Malformed ADR or lesson entry**
- In DECISIONS.md: every `### ADR-NNN` entry must have `**Date**`, `**Status**`, `**Context**`, `**Options considered**`, `**Decision**`, and `**Consequences**`
- In LESSONS_LEARNED.md: every `### LL-NNN` entry must have `**What happened**`, `**Lesson**`, and `**What we do now**`
- Flag numbering gaps or duplicates in either file
- Flag any ADR marked `Superseded by ADR-NNN` where ADR-NNN doesn't exist

**[WARNING] Concept CLAUDE.md missing Concept Specification**
- Every concept CLAUDE.md must have a `## Concept Specification` section with `### State`, `### Actions`, and `### Invariants` subsections
- Flag which subsections are missing

**[WARNING] Concept CLAUDE.md missing Architecture section**
- Every concept CLAUDE.md must have an `## Architecture` section containing an ASCII diagram (look for ` ``` ` block with box-drawing characters or arrows)
- Flag if absent or if the section exists but contains only prose

**[INFO] CHANGELOG.md missing Unreleased section**
- Flag if `CHANGELOG.md` exists but has no `## [Unreleased]` section

**[INFO] SYNCHRONIZATIONS.md has no entries**
- Flag if `SYNCHRONIZATIONS.md` exists but the `## Synchronizations` section contains only the template placeholder (no real SYNC-NNN entries)

---

### Placeholder checks (all docs)

**[WARNING] Unfilled template placeholders in root CLAUDE.md**
- Root CLAUDE.md is loaded into every agent session, so leftover placeholders there are noise the agent reads every time
- Flag lines containing `[Your Project Name]`, `[YYYY-MM-DD]`, `[test command]`, or other `[...]` placeholder text outside code blocks and HTML comments

**[INFO] Unfilled placeholders elsewhere**
- Same check for other docs. Report a count per file rather than every line

---

### Orphan checks

**[WARNING] Concept CLAUDE.md not listed in root CLAUDE.md**
- For every concept CLAUDE.md found, check whether its path appears in the `**Concepts**:` list in the root CLAUDE.md
- Flag concept files that are missing from the list

**[INFO] Doc file with no inbound links**
- For every non-root Markdown file, check whether any other doc links to it
- Flag files that are never referenced (potential orphans or stale docs)

---

## Report Format

```
## Doc Health Report — [date]

### Critical (must fix)
- [file:line] BROKEN LINK: `../CLAUDE.md` → file not found
- [file] MISSING SECTION: root CLAUDE.md has no Key Docs section

### Warnings (should fix)
- [file] STALE DATE: Last Updated 2024-08-01 (>90 days ago)
- [file] ORPHANED: not listed in root CLAUDE.md Concepts list
- [file] MISSING: no isolation rule blockquote

### Info (nice to fix)
- [file] UNRELEASED section empty in CHANGELOG.md
- [file] Never referenced by any other doc

---
X critical · Y warnings · Z info
[N files scanned]
```

---

## Rules

- Never auto-fix Critical or Warning issues without confirmation — show proposed changes first
- Info-level issues may be batch-fixed without per-item confirmation if the user approves
- Do not modify file content to fix a broken link if the target file genuinely doesn't exist — flag it and let the user decide whether to create the file or update the link
- When fixing a stale `Last Updated` date, set it to today's date only — do not infer when the content was actually last changed
- If zero issues are found, say so clearly: "All docs passed health checks."
