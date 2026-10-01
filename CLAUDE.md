# [Your Project Name]

[One or two sentences: what this project does and who it's for.]

**Stack**: [e.g., Python 3.12, pandas, PyTorch, MLflow]

---

## Key Docs

- [PROJECT_PLAN.md](PROJECT_PLAN.md): what we're doing now. Read before starting a feature.
- [DECISIONS.md](DECISIONS.md): why we chose X over Y (ADRs).
- [LESSONS_LEARNED.md](LESSONS_LEARNED.md): what went wrong and what we do differently now.
- [SYNCHRONIZATIONS.md](SYNCHRONIZATIONS.md): cross-concept event flows.
- [ROADMAP.md](ROADMAP.md): longer-term goals.
- [CHANGELOG.md](CHANGELOG.md): what changed, per release.

**Concepts**:
- [Concept name]: `[path/to/concept/CLAUDE.md]`

**Where things get written down**:
- **Choosing between alternatives** → append an ADR to DECISIONS.md (`/decision`). Don't record decisions anywhere else; other docs link to the ADR.
- **Something went wrong that shouldn't happen again** → add to LESSONS_LEARNED.md. If it's about how you (the agent) should work, also add a rule to Conventions below.

---

## Setup & Commands

```bash
[pip install -e ".[dev]" | uv sync | ...]
cp .env.example .env   # then fill in values

[test command]         # e.g. pytest
[lint command]         # e.g. ruff check .
[run command]          # e.g. python -m mypkg.train --config config/baseline.yaml
```

---

## How to Work

- For anything beyond a small fix, **state your plan and assumptions before editing**: which files you'll touch, where new parameters will live, what you'll verify. Wait for a go-ahead if anything is ambiguous.
- Prefer asking over guessing when a convention below doesn't cover the case.
- Keep changes scoped to the task. Mention unrelated problems you notice; don't fix them unasked.

---

## Conventions

Replace these examples with your project's rules. Write them as specific, checkable statements; vague rules ("write clean code") don't change behaviour.

**Parameters & config**
- Tunable values (hyperparameters, thresholds, paths, seeds) live in `config/*.yaml`, loaded into dataclasses in `[src/mypkg]/config.py`.
- Functions take these values as explicit arguments, with no defaults for experiment parameters.
- Notebooks load a config and call functions. No numeric literals or hardcoded paths in notebook cells.
- Adding a parameter means updating the dataclass and the YAML in the same change.

**Plots**
- Create and save figures with `save_figure()` from `[src/mypkg]/plotting.py`. Don't call `plt.savefig()` / `plt.show()` directly.
- Every figure has a title and axis labels (with units). Any axes with more than one series has a legend.

**Code**
- Type hints on public functions. Docstrings state units and array shapes where relevant.
- New functions get a test in `tests/`.

Where you can, enforce a convention in code rather than prose: a figure helper that refuses to save an unlabelled plot, a config model that fails on a missing parameter. See "Enforcing Conventions in Code" in the framework's `docs/ADVANCED_FEATURES.md` for example snippets.

---

## Definition of Done

Before reporting a task as finished:

1. Run the tests and linter; they pass.
2. Re-read your diff against each rule in **Conventions**. List any rule you didn't meet and why.
3. For every figure you created or changed: open the saved image and check it visually.
4. If you chose between alternatives, an ADR exists in DECISIONS.md.
5. Say explicitly what you did **not** verify.

Run `/check-done` to have this checked against the current diff.

---

## Gotchas

Non-obvious things that will trip you up. (Decisions go in DECISIONS.md, not here.)

- **[Short title]**: [What happens and what to do instead.] (`[file:line]`)

---

**Last Updated**: [YYYY-MM-DD]
