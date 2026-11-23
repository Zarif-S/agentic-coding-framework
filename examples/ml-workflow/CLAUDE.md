# ML Workflow - Example Project

<!--
  Example module CLAUDE.md. Claude Code loads it only when working in this folder.
  It holds what the agent can't see from the code: what the module is for, the rules
  that must not break, and the traps. Generate your own with /module-doc.
-->

Turns raw data into a trained, evaluated model. It sits between data loading and deployment; "The system" in the root CLAUDE.md shows the whole flow.

## Must not break

- `raw_data` is never modified after loading; cleaning returns a new frame.
- The train/test split is made once, before anything is fitted, and every later step reuses it.
- Scalers, encoders and imputers are fitted on training rows only.
- All steps in one experiment log to the same `experiment_id`.
- Metric names stay the same across runs of a model type, so runs can be compared.

## Gotchas

- **Features dropped during cleaning fail late**: a feature listed in the experiment config but removed by cleaning only fails at training time. Check the config's feature list against the processed columns first. (`features/select.py`)

## Common tasks

- **Run an experiment**: create `config/experiments/[name].yaml`, run `python train.py --config config/experiments/[name].yaml`, and review it in `mlflow ui`.
- **Add a feature**: implement it in `features/transformers.py`, add its name under `features:` in the experiment config, and check it on a sample before a full run.
- **Add a data source**: write a loader in `data/loaders/[source].py` that returns the expected schema, and register it in `config/data_sources.yaml`.

---

**Last Updated**: 2026-11-23
