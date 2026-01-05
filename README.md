# Cursor Rules

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Universal rules for AI coding assistants in Cursor IDE. A cross-project rule system that adapts to any project using supported technologies through variable-based configuration.

**Features:**
- Variable-based configuration (`${VARIABLE}` syntax) for project-specific values
- Cross-project compatibility — works with any Django, JavaScript, or Makefile-based project
- Modular architecture — enable only the rules you need via `RULE_*` variables

## Installation

### Option A: Cursor Remote Rules

Connect rules directly from GitHub via Cursor settings:

1. Open Cursor Settings (`Cmd/Ctrl + P > Cursor Settings > Rules`)
2. Go to **Rules** → **Remote Rules**
3. Click **Add Remote Rules**
4. Enter repository URL: `https://github.com/Jlosev/cursor-rules.git`

Rules will be automatically synced and updated from the repository.

### Option B: Git Subtree

Embed rules directly into your repository:

> **Note:** Your repository must be initialized (`git init`) and contain at least one commit. `git subtree` requires an existing commit history to merge the subtree into.

```bash
git subtree add --prefix .cursor/rules \
  https://github.com/Jlosev/cursor-rules.git main --squash
```

**Update later:**
```bash
git subtree pull --prefix .cursor/rules \
  https://github.com/Jlosev/cursor-rules.git main --squash
```

**Note:** Alternatively, you can use git submodule or manually copy files to `.cursor/rules/` if preferred.

## Configuration

### Quick Setup with AI

Click to auto-configure rules for your project:

[![Configure cursor-rules](https://img.shields.io/badge/Configure-Cursor_Rules-5A67D8?logo=cursor&style=flat-square)](https://cursor.com/link/prompt?text=I%27ve+added+rules+for+Cursor+agents+to+.cursor%2Frules%2F+from+https%3A%2F%2Fgithub.com%2FJlosev%2Fcursor-rules%0A%0APlease+configure+them+for+my+project%3A%0A%0A1.+Read+project+structure%0A2.+Identify+tech+stack+and+frameworks%0A3.+Create+.cursor%2Frules%2Fproject-config-local.mdc+based+on+project-config-local.example.mdc%0A4.+Fill+all+applicable+fields+from+project+context%0A5.+For+unclear+fields%2C+ask+me+specific+questions%0A6.+Suggest+which+rules+to+disable+if+not+applicable+to+my+stack%0A7.+Add+attribution+badge+to+README.md+%28create+Acknowledgments+section+if+needed%29%3A%0A+++%5B%21%5BCursor+Rules%5D%28https%3A%2F%2Fimg.shields.io%2Fbadge%2FCursor_Rules-Jlosev-5A67D8%3Fstyle%3Dflat-square%29%5D%28https%3A%2F%2Fgithub.com%2FJlosev%2Fcursor-rules%29%0A%0AStart+by+reading+the+project+root+and+key+config+files.)

The agent will:
1. Analyze your project structure
2. Create `project-config-local.mdc`
3. Suggest which rules to enable/disable
4. Add attribution badge to your README

### Manual Configuration

1. Copy template:
   ```bash
   cp project-config-local.example.mdc project-config-local.mdc
   ```

2. Edit with your project values

**Required fields:**
- Project name and type
- Directory paths
- Tech stack

**Optional fields:**
- Service modules
- Test markers
- Makefile commands

## Core Rules (Required)

**`main-rules.mdc`** is mandatory and must always be applied (`alwaysApply: true`). It provides:

- **Role definition**: Sets AI assistant expertise, tone, and behavior for your project
- **Task classification**: Routes tasks to appropriate domain rules via `RULE_*` variables
- **Constraints hierarchy**: CRITICAL → MANDATORY → RECOMMENDED for all operations
- **Rule orchestration**: Connects `project-config-local.mdc` with domain-specific rules

Without `main-rules.mdc`, other rules won't be properly connected or configured.

## Rules Reference

Rules apply automatically based on file paths (`globs`), always (`alwaysApply: true`), or contextually.

### General

| Rule | Description | Pattern | Requires |
|------|-------------|---------|----------|
| `main-rules.mdc` | Core orchestration, role definition | Always | — |
| `mcp-rules.mdc` | MCP server usage priorities | Always | See below |
| `rules-for-rules.mdc` | Meta-rules for creating new rules | `**/*.mdc` | — |

### Backend

| Rule | Description | Pattern | Requires |
|------|-------------|---------|----------|
| `django-backend-rules.mdc` | Django/DRF patterns, ORM optimization | `**/backend/**/*`, `**/*.py` | Django |
| `django-tests-rules.mdc` | pytest, fixtures, markers, ORM testing | `**/test_*.py`, `**/tests/**/*.py` | pytest-django |
| `unfold-rules.mdc` | Django Unfold admin widgets, templates | `**/admin.py`, `**/templates/admin/**/*` | django-unfold |

### Frontend

| Rule | Description | Pattern | Requires |
|------|-------------|---------|----------|
| `js-frontend-rules.mdc` | ES6+ modules, error handling, bundling | `**/client-web/**/*`, `**/*.{js,jsx,ts,tsx}` | — |

### DevOps & Infrastructure

| Rule | Description | Pattern | Requires |
|------|-------------|---------|----------|
| `makefile-rules.mdc` | Make command structure, formatting | `**/Makefile` | — |
| `yc-cli-rules.mdc` | Yandex Cloud CLI patterns | Contextual | yc CLI |

### Documentation

| Rule | Description | Pattern | Requires |
|------|-------------|---------|----------|
| `obsidian-docs-rules.mdc` | Wikilinks, frontmatter, MCP Obsidian | Contextual | MCP Obsidian* |

*Falls back to standard tools if MCP unavailable

### Content & Marketing

| Rule | Description | Pattern | Requires |
|------|-------------|---------|----------|
| `content-editor-rules.mdc` | Infostyle, AIDA, platform specs | Contextual | — |

## Modular Rule Selection

Rules are modular — enable only what you need via `RULE_*` variables in `project-config-local.mdc`.

### Enabling/Disabling Rules

In `project-config-local.mdc`, include only rules you need in the **Active Rules** section:

```markdown
## Active Rules

| Variable | Value |
|----------|-------|
| RULE_BACKEND | django-backend-rules.mdc |
| RULE_FRONTEND | js-frontend-rules.mdc |
<!-- Remove rows for rules you don't need -->
```

### Using Custom Rules

Replace default rule files with your own:

```markdown
## Active Rules

| Variable | Value |
|----------|-------|
| RULE_BACKEND | my-custom-backend-rules.mdc |
| RULE_FRONTEND | js-frontend-rules.mdc |
```

Your custom rule files must follow the same structure as default rules (see `rules-for-rules.mdc`).

## MCP Server Dependencies

Rules work without MCP servers but with reduced functionality.

| Server | Used by | Purpose | Link |
|--------|---------|---------|------|
| Context7 | `mcp-rules.mdc` | Library docs | [context7](https://github.com/upstash/context7) |
| Magic MCP | `mcp-rules.mdc` | React components, UI elements | [magic-mcp](https://github.com/21st-dev/magic-mcp) |
| Playwright | `mcp-rules.mdc` | Browser testing | [playwright-mcp](https://github.com/microsoft/playwright-mcp) |
| Framelink Figma | `mcp-rules.mdc` | Figma design files | [framelink-figma](https://github.com/framelink/framelink-figma) |
| Filesystem | `mcp-rules.mdc` | Extended file ops | [filesystem-mcp](https://github.com/modelcontextprotocol/servers) |
| Obsidian | `obsidian-docs-rules.mdc` | Vault operations, see `obsidian-docs-rules.mdc` for details | [obsidian-mcp](https://github.com/smithery-ai/mcp-obsidian) |

**Fallback**: If MCP unavailable, agent uses standard Cursor tools automatically. For Playwright, falls back to Cursor Browser (`mcp_cursor-ide-browser_*` tools).

## Attribution

This project is MIT licensed — free to use without restrictions.

If you find these rules useful, please consider adding this badge to your README:

[![Cursor Rules](https://img.shields.io/badge/Cursor_Rules-Jlosev-5A67D8?logo=cursor&style=flat-square)](https://github.com/Jlosev/cursor-rules)

**Markdown:**
```markdown
[![Cursor Rules](https://img.shields.io/badge/Cursor_Rules-Jlosev-5A67D8?logo=cursor&style=flat-square)](https://github.com/Jlosev/cursor-rules)
```

Or mention in your Acknowledgments section:
> Cursor rules based on [cursor-rules](https://github.com/Jlosev/cursor-rules) by Jlosev

## Notes

- **Disabling rules**: Change `alwaysApply: false`, remove `globs` and `description` in frontmatter
- **Language**: Rules in English, agent responds in user's language
- **Local overrides**: Create `*-local.mdc` files (auto-excluded via .gitignore)

## Prompting Patterns Used

All rules in this repository follow prompt engineering best practices (2024-2025). See `rules-for-rules.mdc` for full reference.

### Patterns Applied

| Pattern | Description |
|---------|-------------|
| **Hierarchy** | CRITICAL → MANDATORY → RECOMMENDED priority levels |
| **Structure** | Frontmatter → H1 → CONSTRAINTS → Domain → Output → Scope |
| **Output Specification** | Explicit format, length, fields in every rule |
| **Scope & Boundaries** | In scope / Out of scope / Edge cases |
| **Actionable Verbs** | All instructions start with Use, Apply, Avoid, Check |
| **Positive Rewriting** | "Do Y" instead of "Don't X" |
| **Delimiters** | ##, ---, ``` for visual separation |
| **Compression** | Boilerplate removed, prose → bullets/tables |
| **Variables** | `${VAR}` for project-specific values |
| **Examples 0 or 3-5** | Never 1-2 (insufficient for pattern recognition) |
| **Safety Guardrails** | Data instructions treated as text |
| **Confirmation Triggers** | Explicit for destructive operations |
| **Checklists** | Audit + Validation for quality assurance |

### Anti-Patterns Avoided

| Anti-Pattern | Replaced with |
|--------------|---------------|
| CoT phrases ("Let's think...") | Structured sections |
| Model-specific syntax | Universal Markdown |
| ALL CAPS | `**CRITICAL**:` markers |
| Negatives ("Don't X") | Positives ("Do Y") |
| 1-2 examples | 0 or 3-5 |
| Vague instructions | Measurable criteria |
| Passive voice | Active imperatives |
| Boilerplate | Deleted |
| Hardcoded values | `${VARIABLE}` |
| Confidence levels | Confirmation triggers |

Good luck! :)
