# Lessons Learned - [Your Project Name]

What experience taught us: things that went wrong (or unexpectedly right), and what we now do differently.

- **DECISIONS.md** records a choice made *before* acting, with the alternatives.
- **This file** records what we learned *after* acting, and the change it led to.

## Rules

- **Every lesson ends in an action.** A lesson with no "what we do now" is just a complaint. The action is usually a rule, a convention, a test, or a hook.
- **Promote agent-facing lessons.** If the lesson is about how the agent should work (e.g. "plots kept shipping without legends"), also add the rule to the Conventions section of `CLAUDE.md`. That file is loaded every session; this one isn't.
- **Append-only**, numbered `LL-NNN`. Add entries when they happen, or in a batch at the end of a milestone.

---

## Entry Format

```markdown
### LL-NNN: [Short title, phrased as the lesson]

**Date**: YYYY-MM-DD · **Category**: Process | Technical | Agent workflow

**What happened**: [The concrete situation, one to three sentences.]

**Lesson**: [The generalisable takeaway.]

**What we do now**: [The rule, convention, test, or hook that came out of it, and where it lives.]
```

<!--
  EXAMPLE: not a real lesson. Delete once you've added your first entry.

### LL-001: The agent doesn't check plots it can't see

**Date**: YYYY-MM-DD · **Category**: Agent workflow

**What happened**: Several figures were committed without legends or axis units. The code ran, so the agent reported the task as done.

**Lesson**: "Code runs" isn't "output is correct" for visual output. The agent needs to look at the rendered figure.

**What we do now**: Plotting goes through `save_figure()`, which requires a title and axis labels. CLAUDE.md Definition of Done tells the agent to open saved PNGs before finishing.
-->

---

## Lessons

[Add LL entries here, newest at the bottom.]

---

**Related**: [DECISIONS.md](DECISIONS.md) · [CLAUDE.md](CLAUDE.md)
