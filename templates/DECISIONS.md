# Decisions - [Your Project Name]

Architectural decision records (ADRs): **why** we chose X over Y.

- **ROADMAP / PROJECT_PLAN** say where we're going and what we're doing; they get rewritten.
- **CHANGELOG** says *what* changed.
- **This file** keeps the reasoning, including the options we rejected, so it survives after the plan has moved on.

## Rules

- **Append-only.** Never edit the substance of a past entry. If a decision changes, add a new ADR and mark the old one `Superseded by ADR-NNN`.
- **One decision per entry.** Number sequentially (`ADR-001`, `ADR-002`, ...); IDs are stable references for other docs, commits, and PRs.
- **Other docs link here instead of restating.** e.g. PROJECT_PLAN "Why: see ADR-004".
- **When to write one:** whenever we choose between real alternatives and someone could later ask "why X instead of Y?". Use `/decision` to add one.
- **Options show the trade-off.** Each option gets its main pro and con; the point is to see what you give up, not to reach a count. For a dial (a threshold, a ratio), it often helps to weigh the two extremes and a middle option.
- **In one line** is the answer you'd give out loud: the choice, the reason in plain words, and what would change it.
- Keep it short. Five to fifteen lines is normal.

---

## Entry Format

```markdown
### ADR-NNN: [Short title, phrased as the decision]

**Date**: YYYY-MM-DD · **Status**: Accepted | Superseded by ADR-NNN | Deprecated

**Context**: [The situation and constraints at the time. What forced a choice?]

**Options considered**:
- **[Option A]**: [one line: main pro / main con]
- **[Option B]**: [one line: main pro / main con]

**Decision**: [What we chose, in one or two sentences.]

**Consequences**: [What this makes easier, what it makes harder, what we'd revisit and when.]

**In one line**: [The answer you'd give out loud to someone who wasn't there, plus what would change the decision.]
```

<!--
  EXAMPLE: not a real decision. Delete once you've added your first ADR.

### ADR-000: Store experiment parameters in YAML configs, not notebooks

**Date**: YYYY-MM-DD · **Status**: Accepted

**Context**: Parameters were hardcoded across notebook cells, so runs couldn't be reproduced and the agent kept adding new literals in place.

**Options considered**:
- **Notebook literals**: fastest to iterate / not reproducible, values drift between cells
- **Function defaults**: one place per function / hides which values a run actually used
- **YAML + dataclass**: every run's parameters in one file, validated on load / one more file to maintain

**Decision**: YAML configs loaded into a dataclass with no defaults for experiment parameters.

**Consequences**: Every run is reproducible from its config file. Adding a parameter means touching the dataclass and the YAML. Revisit if we adopt a sweep tool with its own config format.

**In one line**: Parameters live in YAML so any run can be reproduced from its config; we'd change this if a sweep tool needs its own format.
-->

---

## Decisions

[Add ADR entries here, newest at the bottom.]

---

**Related**: [ROADMAP.md](ROADMAP.md) · [PROJECT_PLAN.md](PROJECT_PLAN.md) · [LESSONS_LEARNED.md](LESSONS_LEARNED.md)
