# Decisions - Agentic Coding Framework

Architectural decision records for the framework itself: why it is designed the way it is. This is not the template; the copy users take into their projects is [templates/DECISIONS.md](templates/DECISIONS.md), which also defines the entry format used here.

Append-only. If a decision changes, add a new ADR and mark the old one `Superseded by ADR-NNN`.

---

## Decisions

### ADR-001: One append-only DECISIONS.md holds all decision rationale

**Date**: 2026-10-01 · **Status**: Accepted

**Context**: "Why" could be written in four places (ROADMAP, PROJECT_PLAN, root and concept CLAUDE.md), so in practice it was written nowhere. DECISIONS.md was linked from CLAUDE.md but had never been created.

**Options considered**:
- **Keep decision sections in each doc**: rationale sits next to what it explains / four homes means no home, and rewritten plans lose their "why"
- **One DECISIONS.md, others link to ADR IDs**: one place to look and to write / readers follow a link

**Decision**: One append-only DECISIONS.md. ROADMAP's decision section, PROJECT_PLAN's Why fields and concept docs link to ADRs. Concept "Implementation Notes" became "Gotchas". `/decision` writes entries; `/plan-feature` prompts for them.

**Consequences**: Rationale survives plan rewrites. Relies on people running `/decision` at the moment of choice; `/check-done` flags a missing ADR as a backstop.

### ADR-002: Keep LESSONS_LEARNED.md as a template file that feeds Conventions

**Date**: 2026-10-01 · **Status**: Accepted

**Context**: LESSONS_LEARNED.md was referenced but missing. Either create it or remove the references.

**Options considered**:
- **Remove the references**: one fewer file / repeated agent mistakes have nowhere to be recorded
- **Create a template**: mistakes get logged / another file to maintain

**Decision**: Create it. Every entry ends with "what we do now", and lessons about agent behaviour are promoted to a rule in CLAUDE.md Conventions.

**Consequences**: Gives Conventions a source. Only useful if lessons actually get promoted; otherwise it becomes a log nobody reads.

### ADR-003: Remove navigation scaffolding written for weaker models

**Date**: 2026-10-01 · **Status**: Accepted

**Context**: Breadcrumbs, ASCII navigation tables, a structure tree in root CLAUDE.md and a "2–5KB context budget" were written for models that couldn't search a repo well.

**Options considered**:
- **Keep them**: familiar to existing users / they drift out of date and cost context every session
- **Strip them and update the commands that generated them**: less to maintain / agents must find files themselves

**Decision**: Strip them. Root CLAUDE.md keeps a short Key Docs list and a Concepts list. `/doc-health` and `/concept-spec` no longer require or generate breadcrumbs. The guiding principle became "Document what code can't say".

**Consequences**: Smaller, more accurate root CLAUDE.md. Revisit if agents start failing to find docs.

### ADR-004: Convention-enforcing code ships as documented snippets, not a package

**Date**: 2026-10-01 · **Status**: Accepted

**Context**: To show how to enforce conventions in code, an `examples/conventions/` folder was built with `plotting.py`, `config.py`, `demo.py` and tests, then reviewed.

**Options considered**:
- **`examples/conventions/` package with tests**: runnable / `demo.py` faked ML training and confused more than it showed, `plotting.py` only fits matplotlib, the hand-rolled config validator duplicated pydantic, and a template doesn't need its own tests
- **Snippets in `docs/ADVANCED_FEATURES.md` section 7**: short, adaptable, no code to maintain / not importable

**Decision**: Snippets in section 7 (pydantic config, matplotlib `save_figure`). The snippets were run once before being documented.

**Consequences**: Users copy and adapt rather than import. Snippets can rot without tests; re-run them when edited (repo Definition of Done).

### ADR-005: Hooks are documented opt-in examples, not shipped in settings.json

**Date**: 2026-10-01 · **Status**: Accepted

**Context**: A Stop hook (Definition of Done reminder) and a notebook-literals hook enforce conventions the agent keeps skipping.

**Options considered**:
- **Active `.claude/settings.json`**: works immediately / copying `.claude/` into a project would switch hooks on without anyone deciding to
- **Documented examples in `docs/ADVANCED_FEATURES.md` section 8**: an explicit choice per project / one more setup step

**Decision**: Documented, opt-in. No `settings.json` in the repo.

**Consequences**: Users who want them copy two scripts and a settings block. The hook input fields should be checked against current Claude Code docs before enabling.

### ADR-006: /doc-health does not check for rationale outside DECISIONS.md

**Date**: 2026-10-01 · **Status**: Accepted

**Context**: ADR-001 implies a check that flags "why" text written outside DECISIONS.md.

**Options considered**:
- **Add the check**: enforces ADR-001 / it needs fuzzy pattern matching and would produce false positives
- **Drop it**: no noise / relies on `/plan-feature` and `/check-done` prompts instead

**Decision**: Dropped. `/doc-health` checks ADR and lesson format and leftover placeholders only.

**Consequences**: Rationale can still leak into other docs unnoticed. Revisit if that happens often.

### ADR-007: Template files live in templates/, separate from the framework's own docs

**Date**: 2026-10-01 · **Status**: Accepted

**Context**: The repo's root CLAUDE.md was the template, so every session working on the framework loaded placeholder text as instructions, and the framework had nowhere to keep its own decisions.

**Options considered**:
- **Keep templates at the root**: simplest copy commands / framework sessions load placeholders; framework ADRs would ship into every project
- **Move templates to `templates/`; real CLAUDE.md and DECISIONS.md at the root**: clean separation / copy paths change for existing users

**Decision**: Move them. Users copy with `cp -r templates/. your-project/`. `.claude/` stays at the root because the commands are useful when working on the framework too.

**Consequences**: Framework sessions get real instructions. Links from templates to framework docs must use full GitHub URLs. Anyone following the old per-file `cp` commands needs the new path.

### ADR-008: Non-ML Conventions examples live in GETTING_STARTED.md, not the template

**Date**: 2026-10-01 · **Status**: Accepted

**Context**: The template's Conventions examples are data-science specific. RAG/LLM and web projects need their own starting points.

**Options considered**:
- **Add all project types to `templates/CLAUDE.md`**: everything in one place / that file loads into every session, and users would have to delete most of it
- **Separate example blocks in `GETTING_STARTED.md`, linked from the template**: template stays short / one extra click

**Decision**: Example blocks for RAG/LLM and web apps in `GETTING_STARTED.md` ("Conventions examples by project type"), linked by URL from `templates/CLAUDE.md`.

**Consequences**: The template keeps one example set. Add further project types to GETTING_STARTED.md, not the template.
