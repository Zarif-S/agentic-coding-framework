# Deployment - Example Project

<!--
  Example module CLAUDE.md for an event-driven project. This module reacts to events
  from ml-workflow without knowing about it; the reactions are in SYNCHRONIZATIONS.md.
-->

Moves trained models from staging to production, with promotion, rollback and retirement. It knows nothing about how a model was trained; how it reacts to `ml-workflow` is in [SYNCHRONIZATIONS.md](../SYNCHRONIZATIONS.md).

## Must not break

- At most one model is live at any time.
- `promote` runs only when status is `staged`; in any other state it raises.
- `rollback` needs at least one entry in `history`.
- The experiment IDs of staged and production models are kept for audit, even after the model is replaced.
- `history` is append-only; records are never deleted.

## Gotchas

- **`deployment_id` identifies the slot, not the model**: it's assigned once at `stage` and stays the same through promotion, rollback and retirement. Don't regenerate it on `promote`; monitoring, alerts and rollout configs hold references to it. (`deployment/manager.py:42`)
- **One deployment slot**: multi-region or A/B deployments need one `Deployment` object per slot. If slots interact, the interaction is a new entry in SYNCHRONIZATIONS.md. (`deployment/manager.py:1`)

## Common tasks

- **Deploy a new model**: a model is staged automatically when evaluation passes ([SYNC-001](../SYNCHRONIZATIONS.md#sync-001-auto-stage-on-evaluation-pass)). Check it with `python deploy.py status`, then promote it with `python deploy.py promote --deployment-id <id>`.
- **Roll back**: `python deploy.py rollback --deployment-id <id>` restores the latest entry in `history`. If history is empty the command fails; find out why before re-staging.
- **Retire a model**: `python deploy.py retire --deployment-id <id>`. The endpoint returns 503 until a new model is staged and promoted.

---

**Last Updated**: 2026-11-23
