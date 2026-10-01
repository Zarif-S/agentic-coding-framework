# Synchronizations - [Your Project Name]

This document defines all cross-concept event flows.

**Rule**: If an action coordinates between two or more concepts (modules), it belongs here — not inside any individual concept's documentation or code. Concepts must remain independent; this file is the only place where inter-concept relationships are expressed.

---

## How to Read This Document

Each entry follows the pattern from Meng & Jackson (2025):

> **When** `[ConceptA].[action]` fires, **if** [condition], **then** `[ConceptB].[action]` follows.

This mirrors how a synchronization engine routes events between concepts. Concepts have no knowledge of each other — only this file coordinates them.

---

## Synchronizations

### [SYNC-001] [Name]

**Trigger**: `[ConceptA].[action](arg1, arg2)`

**Condition**: [State condition that must hold, or "always"]

**Effects**:
- `[ConceptB].[action](mapped_arg)`
- `[ConceptC].[action](mapped_arg)`

**Rationale**: [Why this coordination is needed. What user-facing behavior does it produce?]

---

### [SYNC-002] [Name]

**Trigger**: `[ConceptA].[action](args)`

**Condition**: [Condition]

**Effects**:
- `[ConceptB].[action](args)`

**Rationale**: [Explanation]

---

## Reference

### What belongs here vs. inside a Concept

| Belongs in Concept CLAUDE.md | Belongs here |
|------------------------------|--------------|
| Internal state transitions | Cross-concept event routing |
| Validation of own inputs | Triggering downstream actions |
| Own invariants and guarantees | Conditional fan-out to multiple concepts |
| Actions on own state | Mapping arguments between concepts |

### When to add a new synchronization

- A user action causes state changes in more than one concept
- One concept's action should trigger another concept's action
- A feature cannot be described by a single concept acting alone

### Naming

Use `[SYNC-NNN]` IDs for stable references in code reviews and cross-linking.

---

**Last Updated**: [YYYY-MM-DD]

**Related**: [ROADMAP.md](ROADMAP.md) · [CLAUDE.md](CLAUDE.md)
