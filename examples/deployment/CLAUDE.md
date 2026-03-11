# Deployment - ML Workflow Example Project

## Breadcrumbs
- **Project setup** → [Root CLAUDE.md](../../CLAUDE.md)
- **Strategic context** → [ROADMAP.md](../../ROADMAP.md)
- **Current sprint** → [PROJECT_PLAN.md](../../PROJECT_PLAN.md)
- **Cross-module flows** → [examples/SYNCHRONIZATIONS.md](../SYNCHRONIZATIONS.md)

> **Isolation rule**: This file describes only what this concept owns. Any coordination with other concepts belongs in SYNCHRONIZATIONS.md — not here.

---

## Concept Specification

**Purpose**: Manage the lifecycle of trained models from staging through production, including promotion, rollback, and retirement.

### State

| Field | Type | Description |
|-------|------|-------------|
| `staged_model` | `Model \| None` | Model candidate awaiting promotion review |
| `staged_experiment_id` | `str \| None` | Experiment ID of the staged model, for traceability |
| `production_model` | `Model \| None` | Currently serving model |
| `production_experiment_id` | `str \| None` | Experiment ID of the production model |
| `deployment_id` | `str` | Unique ID for the current deployment slot |
| `status` | `Literal['idle', 'staged', 'promoting', 'live', 'rolling_back']` | Current lifecycle state |
| `rollout_config` | `RolloutConfig` | Traffic split, canary percentage, health thresholds |
| `history` | `List[DeploymentRecord]` | Ordered log of past production models, for rollback |

### Actions

| Action | Signature | Description |
|--------|-----------|-------------|
| `stage` | `(model: Model, experiment_id: str) → deployment_id: str` | Accept a model candidate; set status to `staged` |
| `promote` | `(deployment_id: str) → None` | Move staged model to production; push previous production to history |
| `rollback` | `(deployment_id: str) → None` | Restore most recent entry from history to production |
| `retire` | `(deployment_id: str) → None` | Remove production model; set status to `idle` |
| `get_status` | `() → DeploymentStatus` | Return current status, deployment_id, and serving model metadata |

### Invariants

- At most one model holds `status = 'live'` at any time
- `promote` can only be called when `status = 'staged'`; calling it in any other state is an error
- `rollback` requires `len(history) > 0`; there must be a previous model to restore
- `staged_experiment_id` and `production_experiment_id` are never cleared — they persist for audit purposes even after the model is replaced
- `history` is append-only; records are never deleted

---

## Architecture

```
        stage(model, experiment_id)
                 ↓
┌────────────────────────────────────────┐
│  status: staged                        │
│  staged_model = model                  │
│  staged_experiment_id = experiment_id  │
└────────────────────────────────────────┘
                 ↓
        promote(deployment_id)
                 ↓
┌────────────────────────────────────────┐
│  status: live                          │
│  production_model = staged_model       │
│  previous model → history              │
└────────────────────────────────────────┘
         ↓                  ↓
  retire(deployment_id)   rollback(deployment_id)
         ↓                  ↓
  status: idle         production_model = history[-1]
```

---

## Common Tasks

### Deploying a new model

1. A model is staged automatically when MLWorkflow evaluation passes — see [SYNC-001](../SYNCHRONIZATIONS.md#sync-001-auto-stage-on-evaluation-pass)
2. Review staged model: `python deploy.py status`
3. Promote manually: `python deploy.py promote --deployment-id <id>`

### Rolling back

```bash
python deploy.py rollback --deployment-id <id>
```

Restores the most recent entry from `history`. If history is empty, the command fails with a clear error — do not attempt to re-stage from scratch without first investigating why history is missing.

### Retiring a model (no replacement ready)

```bash
python deploy.py retire --deployment-id <id>
```

Sets status to `idle`. The serving endpoint will return a 503 until a new model is staged and promoted.

---

## Implementation Notes

### Deployment ID stability

**Issue**: Callers (monitoring, alerts, rollout configs) hold references to a `deployment_id`. If it changes on every promotion, those references break.

**Solution**: `deployment_id` identifies the *slot*, not the model. It is assigned once at `stage` time and remains stable through promotion, rollback, and retirement for that deployment slot.

**Location**: `deployment/manager.py:42`

---

## Known Issues & Solutions

**⚠️ KNOWN LIMITATION: Single deployment slot**
- **Issue**: This concept manages one deployment slot. Multi-region or A/B deployments require multiple slots.
- **Solution/Workaround**: Instantiate separate `Deployment` objects per slot; coordinate via SYNCHRONIZATIONS.md if slots interact.
- **Location**: `deployment/manager.py:1`

---

**Last Updated**: 2026-03-11 | **Status**: Example / Reference | **Maintainer**: Framework
