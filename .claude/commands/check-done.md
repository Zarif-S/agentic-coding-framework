# Check Done

Check the current changes against the project's Conventions and Definition of Done in the root `CLAUDE.md`, and report every gap before the task is called finished.

## Steps

1. **Load the rules** — Read the root `CLAUDE.md` and extract every rule under `## Conventions` and every step under `## Definition of Done`. If either section is missing, say so and stop; there's nothing to check against.

2. **Get the changes** — Run `git status --porcelain` to list changed and untracked files. Then:
   - If the repo has commits (`git rev-parse --verify HEAD` succeeds), run `git diff HEAD` for changes to tracked files.
   - If it has no commits yet, `git diff HEAD` fails; run `git diff --cached` for staged files instead.
   - Untracked files never appear in `git diff`; read each one in full.
   - If nothing has changed, check the most recent commit (`git show HEAD`) and say that's what you're checking. If there are no commits and no changes, say there is nothing to check and stop.

3. **Check each convention against the diff** — Go through the rules one at a time, not as a general impression. For each, decide: `met`, `violated`, or `not applicable`. Common things to look for:
   - Numeric literals or hardcoded paths added to notebook cells (`.ipynb`) or to function defaults where Conventions say they belong in config
   - New parameters added to code but not to the config dataclass and YAML (or the reverse)
   - `plt.savefig` / `plt.show` / `fig.savefig` called directly instead of the project's figure helper
   - Figures created without a title, axis labels, or (for multi-series plots) a legend
   - New public functions without type hints or tests

4. **Check figures visually** — For every image file created or changed in the diff (`.png`, `.jpg`, `.svg`), open it and check that the title, axis labels, units, and legend are present and readable. If the diff changes plotting code but no image was regenerated, flag that the figure wasn't checked.

5. **Run the checks** — Run the test and lint commands listed in the root CLAUDE.md Setup & Commands section. Report pass/fail with the relevant output. If the commands are still placeholders, say so rather than guessing.

6. **Check decisions** — If the diff or the conversation shows a choice between alternatives (a new library, a changed data format, a different approach than the one in PROJECT_PLAN.md), check whether DECISIONS.md has a matching ADR. If not, suggest running `/decision`.

7. **Report** — Use the format below. Do not fix anything yet. Then ask: "Want me to fix the violations?"

---

## Report Format

```
## Check Done — [date]

### Violations
- [rule] → [file:line] [what's wrong]

### Not verified
- [what couldn't be checked and why]

### Passed
- Tests: [pass/fail] · Lint: [pass/fail]
- [N] conventions met · [M] not applicable
- Figures checked: [list]

### Decisions
- [ADR present / suggest /decision for X / none needed]
```

---

## Rules

- Check every convention individually. "Looks fine overall" is not a result
- Quote the file and line for every violation
- Never mark a figure as checked unless you opened the image file
- "Not verified" must list anything you couldn't check, even if everything else passed
- Don't fix anything until the user confirms; this command reports, it doesn't edit
