# Cursor Project Template

A **framework-agnostic** template for AI-assisted development with Cursor. Captures proven development workflow patterns without prescribing a specific tech stack.

## What This Is

This template provides:

- **Development workflow** - Branch-first, clarify, plan, implement, verify
- **Quality enforcement** - Git hooks (Husky) + Cursor CLI hooks for tests and linting
- **Context management** - Session checkpoints, handoff between sessions
- **TDD workflow** - Test-first development rule for new features
- **Design review** - UI/UX review framework with three-level analysis
- **Ideation process** - Structured workflow from idea to implementation plan
- **Auto-formatting** - Automatic code formatting after edits
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
│   │   ├── design-review.mdc        # UI/UX review (description-triggered)
│   │   ├── commit-push-pr.mdc       # Commit and PR workflow (description-triggered)
│   │   ├── test-and-commit.mdc      # Test-first commit (description-triggered)
│   │   └── web-verify.mdc           # Playwright verification (description-triggered)
│   ├── hooks/
│   │   ├── auto-format.py           # Auto-format Python files after edits
│   │   └── implementation-plan-check.py  # Remind to update implementation plans
│   ├── hooks.json                   # Cursor CLI hooks configuration
│   ├── ideation/
│   │   └── IDEATION_PROCESS.md      # Ideation workflow documentation
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

The template uses Husky for quality enforcement at commit time:

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

## Cursor CLI Hooks

The template also uses Cursor's native hooks system (`.cursor/hooks.json`) for AI-aware automation:

| Hook | Trigger | Purpose |
|------|---------|---------|
| `auto-format.py` | After file edit | Auto-format Python files with black/isort |
| `implementation-plan-check.py` | Pre-commit, session end | Remind to update implementation plans for features with ideation docs |

### How Cursor Hooks Work

Cursor CLI hooks run automatically during AI interactions:
- `afterFileEdit`: Runs after the AI edits any file
- `preToolUse`: Runs before specific tools (e.g., Shell for commits)
- `stop`: Runs when the AI session ends

Hook scripts receive environment variables like `CURSOR_FILE_PATH` and `CURSOR_PROJECT_DIR`.

## Development Workflow

1. **BRANCH FIRST** - Create feature branch before any changes
2. **CLARIFY** - Ask questions before coding (especially for UI)
3. **PLAN** - Create implementation plan with steps
4. **IMPLEMENT** - Make incremental changes, run tests frequently
5. **VERIFY** - Run tests, use Playwright for UI changes

## Ideation Process

For complex features, use the structured ideation workflow before implementation:

```
.cursor/ideation/<project-slug>/
├── discovery.md           # Problem space, users, insights
├── requirements.md        # Scope, user stories, success criteria
├── design-language.md     # Visual/interaction principles
├── architecture.md        # Technical approach
├── implementation-plan.md # Epics, stories, acceptance criteria
└── prototypes/            # HTML/CSS prototypes
```

To start ideation:
> "Let's ideate on [your concept]"

See `.cursor/ideation/IDEATION_PROCESS.md` for the full workflow.

## Cursor Rules

The template uses Cursor's `.cursor/rules/` system:

| Rule | Trigger | Purpose |
|------|---------|---------|
| `workflow.mdc` | Always applied | Core development workflow, branching, merge requirements, verification efficiency |
| `context-management.mdc` | Always applied | Session start checks, context checkpoints every 3-5 edits, session handoff, completion checklist |
| `test-first.mdc` | Description-triggered | TDD workflow: write failing tests → implement → verify. Activates on "add/implement/create feature" |
| `design-review.mdc` | Description-triggered | Three-level UI/UX review framework with accessibility checks. Activates on "design review", "review UI" |
| `commit-push-pr.mdc` | Description-triggered | Complete workflow from staged changes to PR creation. Activates on "commit and PR", "create PR" |
| `test-and-commit.mdc` | Description-triggered | Run tests first, only commit if they pass. Activates on "test and commit" |
| `web-verify.mdc` | Description-triggered | Playwright verification for web routes. Activates on "verify routes", "check pages" |

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

### Adding Custom Hooks

Create `.cursor/hooks/your-hook.py`:

```python
#!/usr/bin/env python3
import json
import os

def main():
    file_path = os.environ.get("CURSOR_FILE_PATH", "")
    # Your logic here
    return {"continue": True, "message": "Optional message"}

if __name__ == "__main__":
    print(json.dumps(main()))
```

Then register in `.cursor/hooks.json`:

```json
{
  "afterFileEdit": [
    {"command": "python3 .cursor/hooks/your-hook.py", "timeout": 30}
  ]
}
```

### Adding Patterns

Update `docs/PATTERNS.md` with patterns you learn and want to reuse.

### Project-Specific Config

After the AI scaffolds your project:
- Update `docs/SPEC.md` as the project evolves
- Add project-specific entries to `.gitignore`
- Create project-specific rules in `.cursor/rules/`

## Syncing Improvements from Projects

As you work on projects, you may discover workflow improvements (new hooks, refined rules, better processes). To propagate these back to the templates:

1. Open the project in Claude Code (or Cursor with Claude)
2. Ask: "analyze this project for template improvements" or "sync improvements to templates"
3. Claude will:
   - Compare your project's rules, hooks, and agents against the templates
   - Identify improvements worth propagating
   - Create PRs to update both `claude-project-template` and `cursor-project-template`

No manual logging required - Claude analyzes the diffs on demand.

**What gets synced:**
- Workflow improvements in AGENTS.md or rules
- New or improved hooks
- New rules or agents
- Process documentation updates

**What stays project-specific:**
- BRIEF.md content
- docs/SPEC.md content
- Project-specific rules tied to your tech stack

## Comparison with Claude Code Template

This template is adapted from [claude-project-template](../claude-project-template) for Cursor users.

| Feature | Claude Code | Cursor |
|---------|-------------|--------|
| Project instructions | `CLAUDE.md` | `.cursor/rules/*.mdc` + `AGENTS.md` |
| MCP servers | `.claude/settings.json` | `.cursor/mcp.json` |
| AI-aware hooks | `.claude/settings.json` hooks | `.cursor/hooks.json` |
| Pre-commit checks | Claude hooks (AI-aware) | Git hooks (Husky) + Cursor hooks |
| Branch protection | Blocking hook | Blocking Git hook (`exit 1`) |
| Context checkpoints | Hook-driven reminders | Always-applied rule |
| Session handoff | Blocking hook | Always-applied rule |
| TDD agent | `.claude/agents/test-first.md` | `.cursor/rules/test-first.mdc` |
| Design review agent | `.claude/agents/design-review.md` | `.cursor/rules/design-review.mdc` |
| Ideation process | `.claude/ideation/` | `.cursor/ideation/` |
| Auto-format | afterFileEdit hook | afterFileEdit hook |
| SPEC.md update triggers | Hook-driven | Rule-driven (trigger phrases) |

**Key difference**: Cursor now supports a native hooks system similar to Claude Code. This template uses both Cursor hooks (for AI-aware automation) and traditional Git hooks (Husky) for commit-time enforcement.

## License

MIT - use this template for any project.
