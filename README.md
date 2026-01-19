# Cursor Project Template

A **framework-agnostic** template for AI-assisted development with Cursor. Captures proven development workflow patterns without prescribing a specific tech stack.

## What This Is

This template provides:

- **Development workflow** - Branch-first, clarify, plan, implement, verify
- **Quality enforcement** - Git hooks (Husky) for tests and linting
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
│   │   └── workflow.mdc       # Development workflow rules (always applied)
│   └── mcp.json               # MCP server configuration (Playwright)
├── .husky/
│   └── pre-commit             # Git hook: tests + lint before commit
├── AGENTS.md                  # AI instructions (readable by any AI tool)
├── BRIEF.md                   # Project description (you edit this)
├── docs/
│   ├── SPEC.md                # Technical spec (grows with project)
│   └── PATTERNS.md            # Architectural patterns reference
├── package.json               # For Husky (Git hooks)
├── .gitignore                 # Multi-language patterns
└── README.md                  # This file
```

## Git Hooks (Husky)

The template uses Husky for quality enforcement:

| Hook | Purpose |
|------|---------|
| `pre-commit` | Runs tests + lint, warns about main branch commits |

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

The template uses Cursor's `.cursor/rules/` system:

- `workflow.mdc` - Always-applied workflow rules

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
| Blocking hooks | Yes | No (Git hooks only) |
| Context checkpoints | Built-in reminders | Manual |

**Key difference**: Cursor doesn't have Claude Code's hook system. This template uses traditional Git hooks (Husky) as a fallback, which work but aren't AI-aware.

## License

MIT - use this template for any project.
