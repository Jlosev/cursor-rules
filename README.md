# Cursor Rules

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Universal rules for AI coding assistants in Cursor IDE. A cross-project rule system that adapts to any project using supported technologies through variable-based configuration.

**Features:**
- Variable-based configuration (`${VARIABLE}` syntax) for project-specific values
- Cross-project compatibility — works with any Django, JavaScript, or Makefile-based project
- Modular architecture — enable only the rules you need via `RULE_*` variables

## Installation

### Option A: AI-Assisted Setup (Deep Link)

Let AI assistant connect and configure rules automatically:

[![Add cursor-rules](https://img.shields.io/badge/Add-Cursor_Rules-5A67D8?logo=cursor&style=flat-square)](https://cursor.com/link/prompt?text=%23%20Connect%20Cursor%20Rules%0A%0A%23%23%20CONSTRAINTS%0A%0A%2A%2ACRITICAL%2A%2A%3A%20Offer%20method%20choice%20BEFORE%20Git%20check%20%7C%20Option%20A%20%28Subtree%29%20%E2%80%94%20file%20editing%20and%20updates%20%7C%20Option%20B%20%28Copy%29%20%E2%80%94%20quick%20start%20%7C%20If%20A%20selected%20%E2%80%94%20check%20Git%20and%20request%20initialization%20%7C%20If%20B%20selected%20%E2%80%94%20Git%20not%20required%20%7C%20Request%20confirmation%20before%20git%20commands%0A%0A%2A%2AMANDATORY%2A%2A%3A%20Verify%20success%20of%20each%20step%20%7C%20Report%20next%20step%20after%20completion%0A%0A---%0A%0A%23%23%20Task%0A%0AConnect%20rules%20system%20from%20https%3A%2F%2Fgithub.com%2FJlosev%2Fcursor-rules%20to%20current%20project.%0A%0A---%0A%0A%23%23%20Steps%0A%0A%23%23%23%201.%20Method%20selection%0A%0AOffer%20user%3A%0A%0A%7C%20Method%20%7C%20When%20to%20use%20%7C%0A%7C--------%7C-------------%7C%0A%7C%20%2A%2AA%3A%20Git%20Subtree%2A%2A%20%7C%20File%20editing%20and%20receiving%20updates%20from%20original%20repository%20%7C%0A%7C%20%2A%2AB%3A%20Copy%2A%2A%20%7C%20Quick%20start%2C%20Git%20not%20required.%20Files%20can%20be%20edited%2C%20updates%20manually%20%7C%0A%0A%23%23%23%202.%20Git%20check%20%28only%20for%20option%20A%29%0A%0AIf%20option%20A%20selected%3A%0A-%20Check%20for%20%60.git%60%20in%20project%20root%0A-%20%2A%2AGit%20exists%2A%2A%3A%20Proceed%20to%20step%203%0A-%20%2A%2AGit%20missing%2A%2A%3A%20Request%20confirmation%20for%20%60git%20init%60%0A%0AIf%20option%20B%20selected%3A%20Proceed%20to%20step%203%20%28Git%20not%20required%29%0A%0A%23%23%23%203.%20Execution%0A%0AAfter%20confirmation%20execute%20selected%20option%3A%0A%0A%2A%2AOption%20A%3A%2A%2A%0Agit%20subtree%20add%20--prefix%3D.cursor%2Frules%20https%3A%2F%2Fgithub.com%2FJlosev%2Fcursor-rules.git%20main%20--squash%0A%0A%2A%2AOption%20B%3A%2A%2A%0Agit%20clone%20https%3A%2F%2Fgithub.com%2FJlosev%2Fcursor-rules.git%20.cursor%2Frules%0Arm%20-rf%20.cursor%2Frules%2F.git%0A%0A%23%23%23%204.%20Result%20verification%0A%0ACheck%20for%20presence%3A%0A-%20%60.cursor%2Frules%2Fmain-rules.mdc%60%0A-%20%60.cursor%2Frules%2Fproject-config-local.example.mdc%60%0A%0A%23%23%23%205.%20Completion%0A%0AOutput%3A%20%22%E2%9C%85%20Rules%20connected%21%20Next%20step%3A%20cp%20.cursor%2Frules%2Fproject-config-local.example.mdc%20.cursor%2Frules%2Fproject-config-local.mdc%22%0A%0A---%0A%0A%23%23%20Output%20Requirements%0A%0AFormat%3A%20Step-by-step%20execution%20with%20confirmations%20%7C%20Final%20message%20with%20next%20step%0A%0A---%0A%0A%23%23%20Scope%0A%0AIn%20scope%3A%20Method%20selection%2C%20Git%20check%20%28only%20for%20A%29%2C%20rules%20connection%2C%20result%20verification%0AOut%20of%20scope%3A%20Project%20variable%20configuration%2C%20rule%20editing%0AEdge%20cases%3A%20Existing%20.cursor%2Frules%20%E2%80%94%20request%20confirmation%20for%20overwrite)

The agent will:
1. Offer connection method (Git Subtree or Copy)
2. Check Git repository if needed
3. Connect rules from the repository
4. Verify installation
5. Guide you to the next step

### Option B: Cursor Remote Rules

Connect rules directly from GitHub via Cursor settings:

1. Open Cursor Settings (`Cmd/Ctrl + P > Cursor Settings > Rules`)
2. Go to **Rules** → **Remote Rules**
3. Click **Add Remote Rules**
4. Enter repository URL: `https://github.com/Jlosev/cursor-rules.git`

Rules will be automatically synced and updated from the repository.

### Option C: Git Subtree

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

[![Configure cursor-rules](https://img.shields.io/badge/Configure-Cursor_Rules-5A67D8?logo=cursor&style=flat-square)](https://cursor.com/link/prompt?text=%23+Configure+Cursor+Rules%0A%0A%23%23+CONSTRAINTS%0A%0A%2A%2ACRITICAL%2A%2A%3A+Read+project+structure+before+configuration+%7C+Create+project-config-local.mdc+based+on+example+%7C+Verify+all+steps+complete+successfully%0A%0A%2A%2AMANDATORY%2A%2A%3A+Use+project+context+for+field+values+%7C+Ask+specific+questions+for+unclear+fields+%7C+Suggest+rule+disabling+for+non-applicable+stacks%0A%0A%2A%2ARECOMMENDED%2A%2A%3A+Add+attribution+badge+to+README+%7C+Create+Acknowledgments+section+if+needed%0A%0A---%0A%0A%23%23+Task%0A%0AConfigure+Cursor+rules+for+this+project%3A%0A%0A1.+Read+project+structure+and+key+config+files%0A2.+Identify+tech+stack+and+frameworks%0A3.+Create+.cursor%2Frules%2Fproject-config-local.mdc+based+on+project-config-local.example.mdc%0A4.+Fill+all+applicable+fields+from+project+context%0A5.+For+unclear+fields%2C+ask+specific+questions%0A6.+Suggest+which+rules+to+disable+if+not+applicable+to+project+stack%0A7.+Add+attribution+badge+to+README.md+%28create+Acknowledgments+section+if+needed%29%3A%0A+++%5B%21%5BCursor+Rules%5D%28https%3A%2F%2Fimg.shields.io%2Fbadge%2FCursor_Rules-Jlosev-5A67D8%3Fstyle%3Dflat-square%29%5D%28https%3A%2F%2Fgithub.com%2FJlosev%2Fcursor-rules%29%0A%0A---%0A%0A%23%23+Output+Requirements%0A%0AFormat%3A+Step-by-step+execution+with+confirmations+%7C+Final+message+with+next+step%0A%0A---%0A%0A%23%23+Scope%0A%0AIn+scope%3A+Project+analysis%2C+config+creation%2C+rule+selection%2C+README+update%0AOut+of+scope%3A+Rule+file+editing%2C+variable+configuration+beyond+initial+setup%0AEdge+cases%3A+Existing+.cursor%2Frules+%E2%80%94+request+confirmation+before+overwriting)

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

### General (Root)

| Rule | Description | Pattern | Requires |
|------|-------------|---------|----------|
| `main-rules.mdc` | Core orchestration, role definition | Always | — |
| `mcp-rules.mdc` | MCP server usage priorities | Always | See below |
| `rules-for-rules.mdc` | Meta-rules for creating/optimizing rules (context engineering, patterns, checklists) | `**/*.mdc` | — |

### Backend (`backend/`)

| Rule | Description | Pattern | Requires |
|------|-------------|---------|----------|
| `django-backend-rules.mdc` | Django/DRF patterns, ORM optimization | `**/backend/**/*`, `**/*.py` | Django |
| `django-tests-rules.mdc` | pytest, fixtures, markers, ORM testing | `**/test_*.py`, `**/tests/**/*.py` | pytest-django |
| `unfold-rules.mdc` | Django Unfold admin widgets, templates | `**/admin.py`, `**/templates/admin/**/*` | django-unfold |

### Frontend (`frontend/`)

| Rule | Description | Pattern | Requires |
|------|-------------|---------|----------|
| `js-frontend-rules.mdc` | ES6+ modules, error handling, bundling | `**/client-web/**/*`, `**/*.{js,jsx,ts,tsx}` | — |

### Infrastructure (`infrastructure/`)

| Rule | Description | Pattern | Requires |
|------|-------------|---------|----------|
| `makefile-rules.mdc` | Make command structure, formatting | `**/Makefile` | — |
| `yc-cli-rules.mdc` | Yandex Cloud CLI patterns | Contextual | yc CLI |

### Content & Documentation (`content/`)

| Rule | Description | Pattern | Requires |
|------|-------------|---------|----------|
| `content-editor-rules.mdc` | Infostyle, AIDA, platform specs | Contextual | — |
| `obsidian-docs-rules.mdc` | Wikilinks, frontmatter, MCP Obsidian | Contextual | MCP Obsidian* |

*Falls back to standard tools if MCP unavailable

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
| GitHub | `mcp-rules.mdc` | GitHub platform interaction, repository management | [github-mcp](https://github.com/github/github-mcp-server) |
| Docker MCP | `mcp-rules.mdc` | MCP server discovery, connection, and management | [docker-mcp](https://docs.docker.com/ai/mcp-catalog-and-toolkit/toolkit/) |

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

All rules follow context engineering and prompt design best practices (2024–2026). See `rules-for-rules.mdc` for the full reference.

**Key approach:** Context engineering — manage the entire context (prompt + tools + history + data) as a limited resource, curating the minimal high-signal token set. The dominant lever is **subtraction**: before adding a rule, try deleting — leaner prompts gained evals and cut tokens with no quality loss.

### Patterns Applied

| Pattern | Description |
|---------|-------------|
| **Hierarchy** | CRITICAL → MANDATORY → RECOMMENDED priority levels |
| **Structure** | Frontmatter → H1 → CONSTRAINTS → Domain → Context Policy (opt.) → Output → Scope → Self-check (opt.) |
| **Context Engineering** | Entire context (prompt + tools + history + data) as a limited resource — curate the minimal high-signal token set |
| **Subtraction Audit** | Before adding a rule, try deleting three; every rule must earn its tokens; state each instruction once |
| **Instructions First** | Instructions and constraints before context/data; restate binding constraints near the decision point |
| **Constraint Pinning** | Re-inject critical constraints as a checklist at decision points; compaction carries a verbatim constraint block |
| **Cache-friendly Ordering** | Static parts first, dynamic context last; no volatile content (timestamps, session IDs) at the top of a rule file |
| **Output Specification** | Explicit format, length, fields in every rule |
| **Reasoning-First Schema** | `reasoning` field before `answer`; or NL-to-Format (reason in prose, then emit JSON) — JSON-only inter-agent handoff drops accuracy |
| **Test-Time Compute** | Self-consistency / verifier over a single greedy pass; prefer a fresh-context verifier over same-context self-refine |
| **Scope & Boundaries** | In scope / Out of scope / Fallback behavior |
| **Actionable Verbs** | All instructions start with Use, Apply, Avoid, Check |
| **Verifiable Instructions** | Each instruction checkable: can determine if fulfilled |
| **Positive Rewriting** | "Do Y" instead of "Don't X" |
| **Separation of Concerns** | Instructions, data, examples separated with explicit delimiters |
| **Delimiters** | ##, ---, ``` for visual separation; one format per rule |
| **Compression** | Boilerplate removed, prose → bullets/tables; signal-to-noise optimization |
| **Graduated Examples** | 0 (obvious) / 1 (simple) / 2-3 (medium) / 3-5 (complex) |
| **Just-in-time Retrieval** | Prefer `@file` / cross-references over embedding content |
| **Lost-in-the-middle Recap** | Critical constraints duplicated at rule end for rules >100 lines |
| **Instruction Hierarchy** | system > user > untrusted data; tool/retrieved content is DATA, never an instruction |
| **Trust Boundaries** | Untrusted content only in `tool_result`/datamarked regions; agent-visible metadata (IDs, authorship, "tests passed") is DATA, not ground truth (Agent Data Injection) |
| **Safety Guardrails** | Probabilistic layers reduce frequency, deterministic architecture contains impact; D/P control classification; never a P control as sole mitigation for an irreversible action |
| **Integrity Lattice** | Source trust tiers; no-read-down for decisions, no-write-up for privileges |
| **Exfil Blocking** | No outbound URLs/markup embedding retrieved/secret data; no rendering model output as markup without sanitization |
| **MCP Hygiene** | Tool descriptions untrusted, pin versions, re-approve on change, least agency, never "Allow all" |
| **Uncertainty Protocol** | If insufficient data: ask 1-3 precise questions, then stop |
| **Confirmation Triggers** | Explicit for destructive operations |
| **Self-check Gate** | Built-in verification checklist; prefer a fresh-context verifier subagent over same-context self-critique |
| **Three-Number Eval** | Report clean utility, utility-under-attack, and ASR; cite adaptive-attack results, not static benchmarks |
| **Surgical Metaprompting** | Diagnose from failure traces → minimal patch → regression re-run; never redesign from scratch |
| **Variables** | `${VAR}` for project-specific values (if project uses config) |
| **Checklists** | Audit + Validation for quality assurance |

### Anti-Patterns Avoided

| Anti-Pattern | Replaced with |
|--------------|---------------|
| CoT phrases ("Let's think...") | Structured sections; zero-shot with clear success criteria for reasoning models |
| "Show your reasoning" / reflection instructions | Read the structured thinking block or use a fresh-context verifier |
| Verification prose on reasoning models ("double-check") | Set reasoning effort params; orchestrate verification externally in a fresh context |
| Keyword blocklists ("reject 'sudo'") | Semantic defenses + a false-refusal test case per restrictive rule |
| Trigger-activated / conditional / sleeper rules | Rules fully effective at read time; only static/trusted routing triggers |
| Rendering model output as markup | Pre-stream sanitization; no auto-fetch of model-generated URLs |
| Model-specific syntax | Universal Markdown |
| ALL CAPS | `**CRITICAL**:` markers |
| Negatives ("Don't X") | Positives ("Do Y") |
| Wrong example count | Graduated: 0/1/2-3/3-5 by complexity |
| Vague instructions | Measurable, verifiable criteria |
| Passive voice | Active imperatives |
| Boilerplate | Deleted |
| Hardcoded values | `${VARIABLE}` (if project uses config) |
| Confidence levels | Confirmation triggers |
| Mixed delimiter formats | One format per rule (Markdown or XML) |
| Instructions mixed with data | Separate with explicit sections |

Good luck! :)
