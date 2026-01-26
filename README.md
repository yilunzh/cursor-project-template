# Cursor Project Template

A **framework-agnostic** template for AI-assisted development with Cursor. Captures proven development workflow patterns without prescribing a specific tech stack.

## What This Is

This template provides:

- **Development workflow** - Branch-first, clarify, plan, implement, verify
- **Quality enforcement** - Git hooks (Husky) for tests and linting, branch protection
- **Context management** - Session checkpoints, handoff between sessions
- **TDD workflow** - Test-first development rule for new features
- **Design review** - UI/UX review framework with three-level analysis
- **Pattern documentation** - Reference for common architectural decisions
- **MCP integration** - Playwright for visual verification

## What This Is NOT

- A starter kit with boilerplate code
- A specific tech stack
- A web framework template

**Key insight**: The value isn't in code scaffolding - it's in the AI-assisted development workflow. Let requirements drive technology decisions.

## Getting Started

### 1. Create Your Project

```bash
# Clone template to new project directory
cp -r /path/to/cursor-project-template ~/projects/my-new-project
cd ~/projects/my-new-project

# Initialize git (template doesn't include .git)
git init
git add .
git commit -m "Initial commit from cursor-project-template"

# Install Husky for Git hooks
npm install
```

### 2. Describe Your Project

Edit `BRIEF.md` with a non-technical description of what you're building:

- What is it?
- Why build it?
- For whom?
- Key requirements
- Design inspiration (if UI involved)

### 3. Start Building

Open the project in Cursor:

```bash
cursor .
```

First message to the AI:
> "I'm starting a new project. Read BRIEF.md and help me plan the implementation."

The AI will:
1. Read your brief
2. Ask clarifying questions
3. Recommend a tech stack
4. Create an implementation plan
5. Start building with Git hooks enforcing quality

## Directory Structure

```
cursor-project-template/
├── .cursor/
│   ├── rules/
│   │   ├── workflow.mdc             # Core workflow (always applied)
│   │   ├── context-management.mdc   # Checkpoints & handoff (always applied)
│   │   ├── test-first.mdc           # TDD workflow (description-triggered)
│   │   └── design-review.mdc        # UI/UX review (description-triggered)
│   └── mcp.json                     # MCP server configuration (Playwright)
├── .husky/
│   └── pre-commit                   # Git hook: tests + lint, blocks main commits
├── AGENTS.md                        # AI instructions (readable by any AI tool)
├── BRIEF.md                         # Project description (you edit this)
├── docs/
│   ├── SPEC.md                      # Technical spec (grows with project)
│   └── PATTERNS.md                  # Architectural patterns reference
├── package.json                     # For Husky (Git hooks)
├── .gitignore                       # Multi-language patterns
└── README.md                        # This file
```

## Git Hooks (Husky)

The template uses Husky for quality enforcement:

| Hook | Purpose |
|------|---------|
| `pre-commit` | Runs tests + lint, **blocks** direct commits to main branch |

### Language Detection

The pre-commit hook automatically detects your project type:

- **Python**: pytest, flake8/ruff
- **Node.js**: npm test, eslint
- **Rust**: cargo test, cargo clippy
- **Go**: go test, go vet

### Setup

After cloning:

```bash
npm install  # Installs Husky and sets up hooks
```

## Development Workflow

1. **BRANCH FIRST** - Create feature branch before any changes
2. **CLARIFY** - Ask questions before coding (especially for UI)
3. **PLAN** - Create implementation plan with steps
4. **IMPLEMENT** - Make incremental changes, run tests frequently
5. **VERIFY** - Run tests, use Playwright for UI changes

## Cursor Rules

The template uses Cursor's `.cursor/rules/` system with four rule files:

| Rule | Trigger | Purpose |
|------|---------|---------|
| `workflow.mdc` | Always applied | Core development workflow, branching, merge requirements, verification efficiency |
| `context-management.mdc` | Always applied | Session start checks, context checkpoints every 3-5 edits, session handoff, completion checklist |
| `test-first.mdc` | Description-triggered | TDD workflow: write failing tests → implement → verify. Activates on "add/implement/create feature" |
| `design-review.mdc` | Description-triggered | Three-level UI/UX review framework with accessibility checks. Activates on "design review", "review UI" |

### Rule Types (for customization)

You can add more rules with different behaviors:

```yaml
# Always apply
alwaysApply: true

# Auto-attach when matching files are referenced
globs: ["*.tsx", "*.jsx"]

# AI decides based on description
description: "Rules for React components"
```

## MCP Servers

The template configures Playwright MCP for visual verification:

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["-y", "@playwright/mcp@latest"]
    }
  }
}
```

Use Playwright to screenshot and verify UI changes.

## Customization

### Adding Custom Rules

Create `.cursor/rules/your-rule.mdc`:

```markdown
---
description: "What this rule is for"
alwaysApply: false
globs: ["*.py"]
---

# Rule Content

Instructions for the AI go here.
```

### Adding Patterns

Update `docs/PATTERNS.md` with patterns you learn and want to reuse.

### Project-Specific Config

After the AI scaffolds your project:
- Update `docs/SPEC.md` as the project evolves
- Add project-specific entries to `.gitignore`
- Create project-specific rules in `.cursor/rules/`

## Comparison with Claude Code Template

This template is adapted from [claude-project-template](../claude-project-template) for Cursor users.

| Feature | Claude Code | Cursor |
|---------|-------------|--------|
| Project instructions | `CLAUDE.md` | `.cursor/rules/*.mdc` + `AGENTS.md` |
| MCP servers | `.claude/settings.json` | `.cursor/mcp.json` |
| Pre-commit checks | Claude hooks (AI-aware) | Git hooks (Husky) |
| Branch protection | Blocking hook | Blocking Git hook (`exit 1`) |
| Context checkpoints | Hook-driven reminders | Always-applied rule |
| Session handoff | Blocking hook | Always-applied rule |
| TDD agent | `.claude/agents/test-first.md` | `.cursor/rules/test-first.mdc` |
| Design review agent | `.claude/agents/design-review.md` | `.cursor/rules/design-review.mdc` |
| SPEC.md update triggers | Hook-driven | Rule-driven (trigger phrases) |

**Key difference**: Cursor doesn't have Claude Code's hook system. This template converts hook-driven workflows into Cursor rules (`.cursor/rules/*.mdc`) and uses traditional Git hooks (Husky) for commit-time enforcement.

## License

MIT - use this template for any project.
