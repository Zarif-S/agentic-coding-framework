# Polish

Readability pass on a milestone's code by a fresh agent, then a verification pass by you (the agent that wrote it). The user reads only the polished code, so the polish must not change behaviour unless it says so.

Argument (optional): the files or commit range to polish. Default: uncommitted changes to `.py` files; if there are none, the files changed in `HEAD`.

## Steps

0. **Commit the milestone first** (ask the user before committing). The commit is the baseline: `git diff` shows exactly what the polish changed, `git show HEAD:<path>` gives the old version for probes, `git checkout -- <path>` reverts a bad change, and the milestone and polish commits come apart naturally. No copies of files in the scratchpad. If the user declines, copy the in-scope files to the scratchpad as the baseline instead.

1. **Scope and baseline**
   - List the `.py` files in scope (`git status --porcelain` / `git show --name-only HEAD`). Skip tests unless asked.
   - Run the test and lint commands from CLAUDE.md (e.g. `uv run pytest -q` and `uv run ruff check .`); they must pass before polishing. If not, stop and report.
   - Save baseline output for any script that exercises the code (see Setup & Commands in CLAUDE.md) to the scratchpad. If there is none, say so: tests are then the only behaviour check.
   - List the public names in scope that other modules or tests import (`grep -rn "from <package>.<module> import"`). These must not be renamed.

2. **Polish (subagent, fresh context)** — spawn a `general-purpose` agent with this brief, filling in the file list and protected names:

   > Refactor these files for readability: [files]. The author must explain every line in an interview, so optimise for a reader seeing the code for the first time.
   > Read the "Code style" rules in CLAUDE.md Conventions and the Hard rules first, and follow them: plain functions and dataclasses, no new classes or abstractions, descriptive names (`i`, `n_` are fine), short functions, comments only where the *why* isn't obvious.
   > Do not rename these public names: [names]. Do not edit tests, docs or other files. Do not commit.
   > Keep behaviour identical. If a readability change also changes behaviour (stricter, looser, different error), make it only if it's clearly better, and list it.
   > Finish with: (a) each change and why, one line each; (b) every behaviour change, with an input that shows it; (c) things you considered but left alone.

3. **Verify (you)**
   - Run tests and ruff. Re-run the baseline scripts and `diff` against the saved output; any difference must be explained.
   - Read the full diff (`git diff`). For each behaviour change the subagent listed, probe it with a small input, running old (`git show HEAD:<path>` into the scratchpad) and new side by side. Look for behaviour changes it did *not* list: changed conditions, dropped branches, different exception types or messages, changed defaults.
   - Check the protected names still exist with the same signatures.
   - Check the diff against CLAUDE.md Conventions and Hard rules.

4. **Report** in the format below. Then ask whether to apply your nits and commit. Commit the polish on top of the milestone commit (`Refactor <module> for readability`), and add a line to CHANGELOG.md.

---

## Report Format

```
## Polish review: [files]

**Verdict**: keep / keep with fixes / revert — [one line why]
Tests: pass/fail · Lint: pass/fail · Script output: identical / differs ([why])

### What got better
- [change]: [why it reads better]

### Behaviour changes
| Case | Before | Now | Probed |

### Nits (optional fixes)
1. [what, where, why]

### Subagent's "not done" items
- [item]: act / leave, [why]
```

## Rules

- Never skip the output diff or the probes; the subagent's own summary is not evidence.
- An unlisted behaviour change is a finding even if the new behaviour is better.
- Don't apply nits or commit until the user says so.
