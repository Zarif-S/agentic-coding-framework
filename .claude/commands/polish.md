# Polish

Readability pass on a milestone's code or prose by a fresh agent, then a verification pass by you (the agent that wrote it). The user reads only the polished version, so the polish must not change behaviour (code) or meaning (prose) unless it says so.

Argument (optional): the files or commit range to polish. Default: uncommitted changes to `.py` files; if there are none, the files changed in `HEAD`. Start the argument with `prose` to polish text instead (see Prose mode below).

## Steps

0. **Commit the milestone first** (ask the user before committing). The commit is the baseline: `git diff` shows exactly what the polish changed, `git show HEAD:<path>` gives the old version for probes, `git checkout -- <path>` reverts a bad change, and the milestone and polish commits come apart naturally. No copies of files in the scratchpad. If the user declines, copy the in-scope files to the scratchpad as the baseline instead.

1. **Scope and baseline**
   - List the `.py` files in scope (`git status --porcelain` / `git show --name-only HEAD`). Skip tests unless asked.
   - Run the test and lint commands from CLAUDE.md (e.g. `uv run pytest -q` and `uv run ruff check .`); they must pass before polishing. If not, stop and report.
   - Save baseline output for any script that exercises the code (see Setup & Commands in CLAUDE.md) to the scratchpad. If there is none, say so: tests are then the only behaviour check.
   - List the public names in scope that other modules or tests import (`grep -rn "from <package>.<module> import"`). These must not be renamed.

2. **Polish (subagent, fresh context)** — spawn a `general-purpose` agent with this brief, filling in the file list and protected names:

   > Refactor these files for readability: [files]. The author must be able to explain every line, so optimise for a reader seeing the code for the first time.
   > Read the "Code style" rules in CLAUDE.md Conventions (and any Hard rules section) first, and follow them: plain functions and dataclasses, no new classes or abstractions, descriptive names (`i`, `n_` are fine), short functions, comments only where the *why* isn't obvious.
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

## Prose mode

For Markdown files and the markdown cells of notebooks. Agent-written text tends to be long; this pass shortens it without losing what it says. Step 0 (commit first) applies as above.

1. **Scope and baseline**
   - List changed `.md` files and notebooks (markdown cells only). By default only the sections and cells the diff touched are in scope; a whole file is in scope only when the user names it in the argument. In append-only files (DECISIONS.md, LESSONS_LEARNED.md), only entries added in this milestone are in scope.
   - Save to the scratchpad every number, named reference (file, function, section, ADR or LL ID) and claim in the in-scope text. This list is the baseline for step 3.
   - Note word counts per file.

2. **Polish (subagent, fresh context)** — spawn a `general-purpose` agent with this brief:

   > Shorten and clarify this text: [files, with the sections or cells in scope]. Leave everything else in those files as it is. Follow the Writing section of CLAUDE.md.
   > Cut repetition, filler, hedges that carry no information, and sentences that restate a table or plot sitting next to them.
   > Keep every number, reference and claim. If one is a duplicate, remove it and list it.
   > Don't touch code cells, code blocks, headings other docs link to, or ADR/LL IDs. Don't edit other files. Do not commit.
   > Finish with: (a) word count before and after, per file; (b) each number, reference or claim removed, and why; (c) any sentence whose meaning you changed.

3. **Verify (you)**
   - Check every item on the baseline list: still present, or listed by the subagent as a deliberate removal. Anything else that's missing is a finding.
   - Read the full diff for changed meaning: a hedge removed from a claim that needed it, a qualifier dropped, two points merged into one.
   - Run the link check from CLAUDE.md, if it has one; otherwise check that relative links and anchors in changed files still resolve.

4. **Report** with the prose format below. Ask before committing; commit as `Tighten <files> for readability`.

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

For prose mode:

```
## Prose polish: [files]

**Verdict**: keep / keep with fixes / revert — [one line why]
Words: [before] → [after] · Baseline items kept: [N of M]

### Removed on purpose
- [item]: [why]

### Meaning changes
| Text | Before | Now | Fine? |
```

## Rules

- Never skip the output diff or the probes; the subagent's own summary is not evidence.
- An unlisted behaviour change is a finding even if the new behaviour is better.
- Don't apply nits or commit until the user says so.
