# Synchronizations - ML Workflow Example Project

This document defines all cross-concept event flows.

**Rule**: If an action coordinates between two or more concepts (modules), it belongs here — not inside any individual concept's documentation or code. Concepts must remain independent; this file is the only place where inter-concept relationships are expressed.

---

## How to Read This Document

Each entry follows the pattern from Meng & Jackson (2025):

> **When** `[ConceptA].[action]` fires, **if** [condition], **then** `[ConceptB].[action]` follows.

This mirrors how a synchronization engine routes events between concepts. Concepts have no knowledge of each other — only this file coordinates them.

---

## Synchronizations

### [SYNC-001] Auto-stage on evaluation pass

**Trigger**: `MLWorkflow.evaluate(model, X_test, y_test)`

**Condition**: `metrics['accuracy'] >= rollout_config.promotion_threshold` (default: 0.85)

**Effects**:
- `Deployment.stage(model=model, experiment_id=MLWorkflow.experiment_id)`

**Rationale**: A model that clears the accuracy threshold is a candidate for production. Staging it automatically removes a manual handoff step while still requiring a human `promote` call before it goes live. The threshold lives in `rollout_config`, not in either concept, so changing it doesn't touch MLWorkflow or Deployment code.

---

### [SYNC-002] Archive experiment on promotion

**Trigger**: `Deployment.promote(deployment_id)`

**Condition**: Always

**Effects**:
- `MLWorkflow.archive(experiment_id=Deployment.staged_experiment_id)`

**Rationale**: When a model reaches production, its originating experiment should be marked as the source-of-truth for that deployment. This creates a permanent link between the live model and the experiment run that produced it, enabling reproducibility audits. MLWorkflow has no reason to know about Deployment; Deployment has no reason to know about MLWorkflow — this file is the only place that join is expressed.

---

## Reference

### What belongs here vs. inside a Concept

| Belongs in Concept CLAUDE.md | Belongs here |
|------------------------------|--------------|
| Internal state transitions | Cross-concept event routing |
| Validation of own inputs | Triggering downstream actions |
| Own invariants and guarantees | Conditional fan-out to multiple concepts |
| Actions on own state | Mapping arguments between concepts |

### Why these two concepts don't reference each other

`MLWorkflow` owns training and evaluation. It has no knowledge of whether a model will be deployed, how, or when. `Deployment` owns the serving lifecycle. It has no knowledge of how a model was trained or what data it saw. Each concept can be read, tested, and modified independently.

The coordination — "a passing model gets staged; a promoted model gets archived" — is the only shared knowledge, and it lives entirely in this file. If you add a third concept (e.g., `Monitoring`), its interactions with `Deployment` or `MLWorkflow` get new SYNC entries here, not edits to either concept's doc.

### When to add a new synchronization

- A user action causes state changes in more than one concept
- One concept's action should trigger another concept's action
- A feature cannot be described by a single concept acting alone

### Naming

Use `[SYNC-NNN]` IDs for stable references in code reviews and cross-linking.

---

**Last Updated**: 2026-03-11

**Concepts**: [ml-workflow/CLAUDE.md](ml-workflow/CLAUDE.md) · [deployment/CLAUDE.md](deployment/CLAUDE.md)

**Related**: [Root CLAUDE.md](../CLAUDE.md) · [ROADMAP.md](../ROADMAP.md)
