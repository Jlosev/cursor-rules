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

[![Add cursor-rules](https://img.shields.io/badge/Add-Cursor_Rules-5A67D8?logo=cursor&style=flat-square)](https://cursor.com/link/prompt?text=%23+%D0%9F%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D0%B5+Cursor+Rules%0A%0A%23%23+CONSTRAINTS%0A%0A%2A%2ACRITICAL%2A%2A%3A+%D0%9F%D1%80%D0%B5%D0%B4%D0%BB%D0%BE%D0%B6%D0%B8+%D0%B2%D1%8B%D0%B1%D0%BE%D1%80+%D1%81%D0%BF%D0%BE%D1%81%D0%BE%D0%B1%D0%B0+%D0%9F%D0%95%D0%A0%D0%95%D0%94+%D0%BF%D1%80%D0%BE%D0%B2%D0%B5%D1%80%D0%BA%D0%BE%D0%B9+Git+%7C+%D0%92%D0%B0%D1%80%D0%B8%D0%B0%D0%BD%D1%82+A+%28Subtree%29+%E2%80%94+%D1%80%D0%B5%D0%B4%D0%B0%D0%BA%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5+%D1%84%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2+%D0%B8+%D0%BE%D0%B1%D0%BD%D0%BE%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D1%8F+%7C+%D0%92%D0%B0%D1%80%D0%B8%D0%B0%D0%BD%D1%82+B+%28%D0%9A%D0%BE%D0%BF%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5%29+%E2%80%94+%D0%B1%D1%8B%D1%81%D1%82%D1%80%D1%8B%D0%B9+%D1%81%D1%82%D0%B0%D1%80%D1%82+%7C+%D0%95%D1%81%D0%BB%D0%B8+%D0%B2%D1%8B%D0%B1%D1%80%D0%B0%D0%BD+A+%E2%80%94+%D0%BF%D1%80%D0%BE%D0%B2%D0%B5%D1%80%D1%8C+Git+%D0%B8+%D0%B7%D0%B0%D0%BF%D1%80%D0%BE%D1%81%D0%B8+%D0%B8%D0%BD%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8E+%7C+%D0%95%D1%81%D0%BB%D0%B8+%D0%B2%D1%8B%D0%B1%D1%80%D0%B0%D0%BD+B+%E2%80%94+Git+%D0%BD%D0%B5+%D1%82%D1%80%D0%B5%D0%B1%D1%83%D0%B5%D1%82%D1%81%D1%8F+%7C+%D0%97%D0%B0%D0%BF%D1%80%D0%BE%D1%81%D0%B8+%D0%BF%D0%BE%D0%B4%D1%82%D0%B2%D0%B5%D1%80%D0%B6%D0%B4%D0%B5%D0%BD%D0%B8%D0%B5+%D0%BF%D0%B5%D1%80%D0%B5%D0%B4+git+%D0%BA%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0%D0%BC%D0%B8%0A%0A%2A%2AMANDATORY%2A%2A%3A+%D0%9F%D1%80%D0%BE%D0%B2%D0%B5%D1%80%D1%8C+%D1%83%D1%81%D0%BF%D0%B5%D1%88%D0%BD%D0%BE%D1%81%D1%82%D1%8C+%D0%BA%D0%B0%D0%B6%D0%B4%D0%BE%D0%B3%D0%BE+%D1%88%D0%B0%D0%B3%D0%B0+%7C+%D0%A1%D0%BE%D0%BE%D0%B1%D1%89%D0%B8+%D0%BE+%D1%81%D0%BB%D0%B5%D0%B4%D1%83%D1%8E%D1%89%D0%B5%D0%BC+%D1%88%D0%B0%D0%B3%D0%B5+%D0%BF%D0%BE%D1%81%D0%BB%D0%B5+%D0%B7%D0%B0%D0%B2%D0%B5%D1%80%D1%88%D0%B5%D0%BD%D0%B8%D1%8F%0A%0A---%0A%0A%23%23+%D0%97%D0%B0%D0%B4%D0%B0%D1%87%D0%B0%0A%0A%D0%9F%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D1%8C+%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D1%83+%D0%BF%D1%80%D0%B0%D0%B2%D0%B8%D0%BB+%D0%B8%D0%B7+https%3A%2F%2Fgithub.com%2FJlosev%2Fcursor-rules+%D0%BA+%D1%82%D0%B5%D0%BA%D1%83%D1%89%D0%B5%D0%BC%D1%83+%D0%BF%D1%80%D0%BE%D0%B5%D0%BA%D1%82%D1%83.%0A%0A---%0A%0A%23%23+%D0%A8%D0%B0%D0%B3%D0%B8%0A%0A%23%23%23+1.+%D0%92%D1%8B%D0%B1%D0%BE%D1%80+%D1%81%D0%BF%D0%BE%D1%81%D0%BE%D0%B1%D0%B0+%D0%BF%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D1%8F%0A%0A%D0%9F%D1%80%D0%B5%D0%B4%D0%BB%D0%BE%D0%B6%D0%B8+%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8E%3A%0A%0A%7C+%D0%A1%D0%BF%D0%BE%D1%81%D0%BE%D0%B1+%7C+%D0%9A%D0%BE%D0%B3%D0%B4%D0%B0+%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D1%82%D1%8C+%7C%0A%7C--------%7C-------------------%7C%0A%7C+%2A%2AA%3A+Git+Subtree%2A%2A+%7C+%D0%A0%D0%B5%D0%B4%D0%B0%D0%BA%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5+%D1%84%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2+%D0%B8+%D0%BF%D0%BE%D0%BB%D1%83%D1%87%D0%B5%D0%BD%D0%B8%D0%B5+%D0%BE%D0%B1%D0%BD%D0%BE%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B9+%D0%B8%D0%B7+%D0%BE%D1%80%D0%B8%D0%B3%D0%B8%D0%BD%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE%D0%B3%D0%BE+%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D1%8F+%7C%0A%7C+%2A%2AB%3A+%D0%9A%D0%BE%D0%BF%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5%2A%2A+%7C+%D0%91%D1%8B%D1%81%D1%82%D1%80%D1%8B%D0%B9+%D1%81%D1%82%D0%B0%D1%80%D1%82%2C+Git+%D0%BD%D0%B5+%D1%82%D1%80%D0%B5%D0%B1%D1%83%D0%B5%D1%82%D1%81%D1%8F.+%D0%A4%D0%B0%D0%B9%D0%BB%D1%8B+%D0%BC%D0%BE%D0%B6%D0%BD%D0%BE+%D1%80%D0%B5%D0%B4%D0%B0%D0%BA%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D1%82%D1%8C%2C+%D0%BE%D0%B1%D0%BD%D0%BE%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D1%8F+%D0%B2%D1%80%D1%83%D1%87%D0%BD%D1%83%D1%8E+%7C%0A%0A%23%23%23+2.+%D0%9F%D1%80%D0%BE%D0%B2%D0%B5%D1%80%D0%BA%D0%B0+Git+%28%D1%82%D0%BE%D0%BB%D1%8C%D0%BA%D0%BE+%D0%B4%D0%BB%D1%8F+%D0%B2%D0%B0%D1%80%D0%B8%D0%B0%D0%BD%D1%82%D0%B0+A%29%0A%0A%D0%95%D1%81%D0%BB%D0%B8+%D0%B2%D1%8B%D0%B1%D1%80%D0%B0%D0%BD+%D0%B2%D0%B0%D1%80%D0%B8%D0%B0%D0%BD%D1%82+A%3A%0A-+%D0%9F%D1%80%D0%BE%D0%B2%D0%B5%D1%80%D1%8C+%D0%BD%D0%B0%D0%BB%D0%B8%D1%87%D0%B8%D0%B5+%60.git%60+%D0%B2+%D0%BA%D0%BE%D1%80%D0%BD%D0%B5+%D0%BF%D1%80%D0%BE%D0%B5%D0%BA%D1%82%D0%B0%0A-+%2A%2AGit+%D0%B5%D1%81%D1%82%D1%8C%2A%2A%3A+%D0%9F%D0%B5%D1%80%D0%B5%D1%85%D0%BE%D0%B4%D0%B8+%D0%BA+%D1%88%D0%B0%D0%B3%D1%83+3%0A-+%2A%2AGit+%D0%BD%D0%B5%D1%82%2A%2A%3A+%D0%97%D0%B0%D0%BF%D1%80%D0%BE%D1%81%D0%B8+%D0%BF%D0%BE%D0%B4%D1%82%D0%B2%D0%B5%D1%80%D0%B6%D0%B4%D0%B5%D0%BD%D0%B8%D0%B5+%D0%BD%D0%B0+%60git+init%60%0A%0A%D0%95%D1%81%D0%BB%D0%B8+%D0%B2%D1%8B%D0%B1%D1%80%D0%B0%D0%BD+%D0%B2%D0%B0%D1%80%D0%B8%D0%B0%D0%BD%D1%82+B%3A+%D0%9F%D0%B5%D1%80%D0%B5%D1%85%D0%BE%D0%B4%D0%B8+%D0%BA+%D1%88%D0%B0%D0%B3%D1%83+3+%28Git+%D0%BD%D0%B5+%D1%82%D1%80%D0%B5%D0%B1%D1%83%D0%B5%D1%82%D1%81%D1%8F%29%0A%0A%23%23%23+3.+%D0%92%D1%8B%D0%BF%D0%BE%D0%BB%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5%0A%0A%D0%9F%D0%BE%D1%81%D0%BB%D0%B5+%D0%BF%D0%BE%D0%B4%D1%82%D0%B2%D0%B5%D1%80%D0%B6%D0%B4%D0%B5%D0%BD%D0%B8%D1%8F+%D0%B2%D1%8B%D0%BF%D0%BE%D0%BB%D0%BD%D0%B8+%D0%B2%D1%8B%D0%B1%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9+%D0%B2%D0%B0%D1%80%D0%B8%D0%B0%D0%BD%D1%82%3A%0A%0A%2A%2A%D0%92%D0%B0%D1%80%D0%B8%D0%B0%D0%BD%D1%82+A%3A%2A%2A%0Agit+subtree+add+--prefix%3D.cursor%2Frules+https%3A%2F%2Fgithub.com%2FJlosev%2Fcursor-rules.git+main+--squash%0A%0A%2A%2A%D0%92%D0%B0%D1%80%D0%B8%D0%B0%D0%BD%D1%82+B%3A%2A%2A%0Agit+clone+https%3A%2F%2Fgithub.com%2FJlosev%2Fcursor-rules.git+.cursor%2Frules%0Arm+-rf+.cursor%2Frules%2F.git%0A%0A%23%23%23+4.+%D0%9F%D1%80%D0%BE%D0%B2%D0%B5%D1%80%D0%BA%D0%B0+%D1%80%D0%B5%D0%B7%D1%83%D0%BB%D1%8C%D1%82%D0%B0%D1%82%D0%B0%0A%0A%D0%9F%D1%80%D0%BE%D0%B2%D0%B5%D1%80%D1%8C+%D0%BD%D0%B0%D0%BB%D0%B8%D1%87%D0%B8%D0%B5%3A%0A-+%60.cursor%2Frules%2Fmain-rules.mdc%60%0A-+%60.cursor%2Frules%2Fproject-config-local.example.mdc%60%0A%0A%23%23%23+5.+%D0%97%D0%B0%D0%B2%D0%B5%D1%80%D1%88%D0%B5%D0%BD%D0%B8%D0%B5%0A%0A%D0%92%D1%8B%D0%B2%D0%B5%D0%B4%D0%B8%3A+%22%E2%9C%85+%D0%9F%D1%80%D0%B0%D0%B2%D0%B8%D0%BB%D0%B0+%D0%BF%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D1%8B%21+%D0%A1%D0%BB%D0%B5%D0%B4%D1%83%D1%8E%D1%89%D0%B8%D0%B9+%D1%88%D0%B0%D0%B3%3A+cp+.cursor%2Frules%2Fproject-config-local.example.mdc+.cursor%2Frules%2Fproject-config-local.mdc%22%0A%0A---%0A%0A%23%23+Output+Requirements%0A%0AFormat%3A+%D0%9F%D0%BE%D1%88%D0%B0%D0%B3%D0%BE%D0%B2%D0%BE%D0%B5+%D0%B2%D1%8B%D0%BF%D0%BE%D0%BB%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5+%D1%81+%D0%BF%D0%BE%D0%B4%D1%82%D0%B2%D0%B5%D1%80%D0%B6%D0%B4%D0%B5%D0%BD%D0%B8%D1%8F%D0%BC%D0%B8+%7C+%D0%A4%D0%B8%D0%BD%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE%D0%B5+%D1%81%D0%BE%D0%BE%D0%B1%D1%89%D0%B5%D0%BD%D0%B8%D0%B5+%D1%81%D0%BE+%D1%81%D0%BB%D0%B5%D0%B4%D1%83%D1%8E%D1%89%D0%B8%D0%BC+%D1%88%D0%B0%D0%B3%D0%BE%D0%BC%0A%0A---%0A%0A%23%23+Scope%0A%0AIn+scope%3A+%D0%92%D1%8B%D0%B1%D0%BE%D1%80+%D1%81%D0%BF%D0%BE%D1%81%D0%BE%D0%B1%D0%B0%2C+%D0%BF%D1%80%D0%BE%D0%B2%D0%B5%D1%80%D0%BA%D0%B0+Git+%28%D1%82%D0%BE%D0%BB%D1%8C%D0%BA%D0%BE+%D0%B4%D0%BB%D1%8F+A%29%2C+%D0%BF%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D0%B5+%D0%BF%D1%80%D0%B0%D0%B2%D0%B8%D0%BB%2C+%D0%BF%D1%80%D0%BE%D0%B2%D0%B5%D1%80%D0%BA%D0%B0+%D1%80%D0%B5%D0%B7%D1%83%D0%BB%D1%8C%D1%82%D0%B0%D1%82%D0%B0%0AOut+of+scope%3A+%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0+%D0%BF%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%BD%D1%8B%D1%85+%D0%BF%D1%80%D0%BE%D0%B5%D0%BA%D1%82%D0%B0%2C+%D1%80%D0%B5%D0%B4%D0%B0%D0%BA%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5+%D0%BF%D1%80%D0%B0%D0%B2%D0%B8%D0%BB%0AEdge+cases%3A+%D0%A1%D1%83%D1%89%D0%B5%D1%81%D1%82%D0%B2%D1%83%D1%8E%D1%89%D0%B0%D1%8F+.cursor%2Frules+%E2%80%94+%D0%B7%D0%B0%D0%BF%D1%80%D0%BE%D1%81%D0%B8%D1%82%D1%8C+%D0%BF%D0%BE%D0%B4%D1%82%D0%B2%D0%B5%D1%80%D0%B6%D0%B4%D0%B5%D0%BD%D0%B8%D0%B5+%D0%BD%D0%B0+%D0%BF%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D0%B8%D1%81%D1%8C)

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
