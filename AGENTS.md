# AGENTS.md

This file provides guidance to AI coding assistants (Cursor, Claude Code, etc.) when working with code in this repository.

## Project Overview

See `BRIEF.md` for the project description and `docs/SPEC.md` for the technical specification.

## Development Workflow

### Phase 0: BRANCH FIRST

Before making ANY changes:

1. Check current branch: `git branch --show-current`
2. For new features: `git checkout -b feature/<feature-name>`
3. For bug fixes: `git checkout -b fix/<bug-description>`
4. **NEVER commit directly to main** - All changes go through branches → PR

#### Merge Requirements

Before merging any PR:
1. All CI checks must pass
2. Wait for checks to complete — do NOT merge while checks are "in progress"
3. If CI fails — fix issues in the branch, push, wait for CI again

### Phase 1: CLARIFY FIRST

Before writing implementation code:

1. **Read related code** - Understand existing patterns
2. **Ask clarifying questions** about:
   - Ambiguous requirements
   - User-facing text (error messages, labels)
   - Edge cases
   - Scope boundaries
3. **Wait for answers** - Don't assume

For UI features, also clarify: design inspiration, visual style, component library preference.

### Phase 2: PLAN

Create an implementation plan:
- Implementation steps
- Test steps
- Verification step

### Phase 3: IMPLEMENT

Proceed autonomously:
1. Make incremental changes
2. Run related tests after each change
3. Fix failures immediately

#### Context Checkpoints

**Every 3-5 major code edits**, update `.cursor/session-context.md` with:

```markdown
## Current Goal
What we're trying to accomplish

## Decisions Made
- Key choice 1 and rationale
- Key choice 2 and rationale

## Files Modified
- file1.py - what changed
- file2.html - what changed

## What's Next
- Remaining step 1
- Remaining step 2
```

All four sections are required. Update proactively — don't wait to be asked.

For multi-session work, write `.cursor/handoff.md` before ending with the same sections. Resume with "continue from handoff".

### Phase 4: VERIFY

Before claiming done:
1. Run tests - all must pass
2. If user-facing changes: present for review
3. For UI: verify pages load correctly using Playwright MCP (`browser_navigate` + `browser_snapshot`)

#### Verification Efficiency

- **Define "done" upfront**: Identify what verification is needed before starting. Once met, stop.
- **Trust existing tests**: If a relevant test passes, that's sufficient. Don't duplicate.
- **One verification path**: Choose either existing test OR manual check. Not both.
- **Don't over-verify**: Sufficient verification = done.

## Decision Guidelines

### Ask User First
- User-facing changes (UI, messages, outputs)
- API contracts and data formats
- Error messages and notifications
- Visual design decisions
- Security-sensitive changes
- Breaking changes

### Proceed Autonomously
- Internal refactoring
- Bug fixes with clear solutions
- Test improvements
- Performance optimizations
- Code organization

## Quality Enforcement

This project uses multiple quality mechanisms:

- **Git hooks (Husky)**: Pre-commit hook runs tests and lint before each commit
- **Branch protection**: Pre-commit hook blocks direct commits to main branch
- **Language-agnostic**: Hook auto-detects Python, Node.js, Rust, Go
- **Cursor rules**: `.cursor/rules/` contains workflow, context management, TDD, and design review rules

To set up hooks after cloning:
```bash
npm install  # Installs Husky
```

## SPEC.md Updates

After completing a feature, update `docs/SPEC.md`. Trigger phrases:
- "feature complete", "update spec", "update documentation"
- "spec update", "document this feature"

**Update workflow:**
1. Review recent git changes (`git diff`, `git log`) to understand what was built
2. Update the relevant sections of `docs/SPEC.md`:
   - Add feature to "Implemented" section
   - Document key architectural decisions
   - Update "Current State" as needed
   - Add new entries to "Version History" table
3. Commit the SPEC update to the current branch

## Reference Documentation

- `BRIEF.md` - Project description (non-technical)
- `docs/SPEC.md` - Technical specification
- `docs/PATTERNS.md` - Architectural patterns reference

## Cursor Rules

The `.cursor/rules/` directory contains AI-specific rules:

| File | Trigger | Purpose |
|------|---------|---------|
| `workflow.mdc` | Always applied | Core development workflow, branching, verification |
| `context-management.mdc` | Always applied | Session checkpoints, handoff, completion checks |
| `test-first.mdc` | Description-triggered | TDD workflow for new features |
| `design-review.mdc` | Description-triggered | UI/UX design review framework |
