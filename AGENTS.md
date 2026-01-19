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

### Phase 4: VERIFY

Before claiming done:
1. Run tests - all must pass
2. If user-facing changes: present for review
3. For UI: verify pages load correctly

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

This project uses Git hooks (Husky) for quality enforcement:

- **Pre-commit hook** runs tests and lint before each commit
- Hook warns (but allows) commits to main branch
- Language-agnostic: auto-detects Python, Node.js, Rust, Go

To set up hooks after cloning:
```bash
npm install  # Installs Husky
```

## Reference Documentation

- `BRIEF.md` - Project description (non-technical)
- `docs/SPEC.md` - Technical specification
- `docs/PATTERNS.md` - Architectural patterns reference

## After Completing Features

Update `docs/SPEC.md`:
- Add feature to "Implemented" section
- Document key architectural decisions
- Update "Current State" as needed
