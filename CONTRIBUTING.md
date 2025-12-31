# Contributing to Agentic Coding Framework

Thank you for your interest in improving this framework! This guide will help you contribute effectively.

---

## How to Contribute

### Reporting Issues

**Found a problem?**
- Check [existing issues](https://github.com/your-username/agentic-coding-framework/issues) first
- Create a new issue with:
  - Clear title describing the problem
  - Steps to reproduce (if applicable)
  - What you expected vs what happened
  - Suggestions for improvement (optional)

**Ideas for improvements?**
- Open an issue labeled "enhancement"
- Describe the use case and why it would help
- Share examples from your experience

---

## Contributing Changes

### 1. Fork and Clone

```bash
# Fork the repository on GitHub, then:
git clone https://github.com/your-username/agentic-coding-framework.git
cd agentic-coding-framework
git remote add upstream https://github.com/original-owner/agentic-coding-framework.git
```

### 2. Create a Branch

```bash
# Create a branch for your changes
git checkout -b feature/your-feature-name

# Or for bug fixes
git checkout -b fix/issue-description
```

### 3. Make Your Changes

**When updating templates**:
- Ensure changes work across different project types (small, medium, large teams)
- Update examples to reflect changes
- Test templates in a real project if possible

**When updating documentation**:
- Use clear, concise language
- Add examples where helpful
- Maintain consistent formatting with existing docs

### 4. Test Your Changes

**Manual testing**:
- Copy templates to a test project
- Verify all links work
- Check that examples are accurate
- Ensure breadcrumbs navigate correctly

**Checklist**:
- [ ] All internal links work
- [ ] Examples are accurate and helpful
- [ ] Formatting is consistent
- [ ] No contradictions with other docs

### 5. Commit Your Changes

```bash
# Stage your changes
git add .

# Commit with a clear message
git commit -m "Add feature: [brief description]

- [Change 1]
- [Change 2]
- [Change 3]
```

**Commit message format**:
- Use present tense ("Add feature" not "Added feature")
- First line: Brief summary (50 chars or less)
- Blank line, then bullet points with details

### 6. Push and Create PR

```bash
# Push to your fork
git push origin feature/your-feature-name
```

Then create a Pull Request on GitHub with:
- Clear title describing the change
- Description of what changed and why
- Link to any related issues
- Screenshots if UI/formatting changed

---

## Types of Contributions We're Looking For

### 🌟 High Value

- **Real-world usage reports**: Share how you adapted the framework
- **New advanced patterns**: Patterns you discovered that work well
- **Improved examples**: Better examples that clarify concepts
- **Clarity improvements**: Make confusing sections clearer

### ✅ Always Welcome

- **Bug fixes**: Broken links, incorrect examples, typos
- **Documentation improvements**: Better explanations, missing context
- **Template enhancements**: Improvements to CLAUDE.md, ROADMAP.md, etc.

### 🤔 Discuss First (Open Issue)

- **Major structural changes**: Changes to core framework philosophy
- **New core documents**: Adding new required files beyond current set
- **Automation tools**: Scripts, validators, GitHub Actions
- **Breaking changes**: Changes that would require users to restructure

---

## Framework Philosophy

When contributing, keep these principles in mind:

### 1. Context Efficiency Over Completeness
- AI agents need focused context, not exhaustive docs
- 2-5KB of targeted docs > 50KB of comprehensive docs
- Task-oriented navigation over encyclopedic coverage

### 2. Flexible Guidelines, Not Rigid Rules
- Provide guidance, not strict requirements
- Allow adaptation to different project needs
- Optimize for findability, not purity

### 3. Zero Workflow Interruption
- Documentation helps development, doesn't hinder it
- Batch updates, don't pause work for docs
- Use severity levels (only critical issues interrupt)

### 4. Progressive Disclosure
- **Tier 1 (Core)**: Essential for every project
- **Tier 2 (Advanced)**: Optional patterns for specific needs
- Start simple, add complexity only when needed

---

## Review Process

### What Reviewers Look For

1. **Alignment with philosophy**: Does this fit the framework's goals?
2. **Clarity**: Is it easy to understand?
3. **Examples**: Are there concrete examples showing how to use it?
4. **Completeness**: Does it cover edge cases?
5. **Consistency**: Does it match existing style and structure?

### Timeline

- **Small changes** (typos, links): Merged within 1-3 days
- **Medium changes** (new sections): Reviewed within 1 week
- **Large changes** (new patterns): Discussed first, then reviewed

### Feedback

We aim for:
- ✅ Constructive, specific feedback
- ✅ Suggestions for improvement, not just criticism
- ✅ Recognition of good ideas, even if implementation needs work

---

## Code of Conduct

### Our Standards

- **Be respectful**: Different projects have different needs
- **Be helpful**: Provide context and examples
- **Be open**: Consider perspectives from different team sizes/types
- **Be constructive**: Suggest improvements, not just problems

### Unacceptable Behavior

- Personal attacks or harassment
- Dismissive or condescending comments
- Bad faith arguments or trolling

### Enforcement

Violations of the code of conduct may result in:
1. Warning and request to modify behavior
2. Temporary ban from contributing
3. Permanent ban for severe or repeated violations

Report issues to: [maintainer email or GitHub reporting mechanism]

---

## Getting Help

**Questions about the framework?**
- Check existing documentation first
- Search [closed issues](https://github.com/your-username/agentic-coding-framework/issues?q=is%3Aissue+is%3Aclosed)
- Open a new issue with the "question" label

**Questions about your PR?**
- Comment on the PR
- Maintainers will respond within a few days

**Want to discuss a big idea?**
- Open an issue first before implementing
- We'll discuss feasibility and approach

---

## Recognition

Contributors will be:
- Listed in release notes for their contributions
- Acknowledged in the README (for significant contributions)
- Credited in commit messages

---

## License

By contributing, you agree that your contributions will be licensed under the MIT License (see [LICENSE](LICENSE)).

---

## Questions?

Not sure if your idea fits? **Open an issue and ask!** We're happy to discuss before you spend time implementing.

Thank you for helping make documentation better for the AI agent era!

---

**Related Documentation**:
- [README.md](README.md) - Framework overview
- [docs/ADVANCED_FEATURES.md](docs/ADVANCED_FEATURES.md) - Advanced patterns and features
