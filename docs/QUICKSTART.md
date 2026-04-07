# Quickstart

Get nv:context running in 2 minutes.

> **See it live:** [skills.nichevlabs.com](https://skills.nichevlabs.com) shows production case studies, the research library, and the full synthesis.

## Install

### Option 1: Skills CLI (recommended)

```bash
npx skills add johnnichev/nv-context -g -y
```

### Option 2: One-liner

```bash
mkdir -p ~/.claude/skills/nv-context && curl -o ~/.claude/skills/nv-context/SKILL.md \
  https://raw.githubusercontent.com/johnnichev/nv-context/main/skills/nv-context/SKILL.md
```

### Option 3: Clone with templates

```bash
git clone https://github.com/johnnichev/nv-context.git
mkdir -p ~/.claude/skills/nv-context
cp -r nv-context/skills/nv-context/* ~/.claude/skills/nv-context/
```

## Use

Open Claude Code in your repo and run:

```
/nv-context
```

The skill will:
1. Ask you about your tools, team, pain points, and landmines (~2 min)
2. Analyze your codebase (~30 sec)
3. Score your current maturity and leverage
4. Generate tailored config files
5. Set up hooks, session management, and token budgets
6. Report what was created and what to hand-refine

## What Gets Generated

Depends on your answers, but typically:

```
your-repo/
  AGENTS.md                    # Universal config (all AI tools read this)
  CLAUDE.md                    # Claude-specific with @imports
  tests/CLAUDE.md              # Testing scope
  src/CLAUDE.md                # Source scope
  HANDOFF.md                   # Session handoff template
  .claudeignore                # Exclude irrelevant files
  .claude/
    settings.local.json        # Hooks (auto-format, branch protection, etc.)
  .cursor/rules/               # Cursor scoped rules (if you use Cursor)
  .github/
    copilot-instructions.md    # Copilot config (if you use Copilot)
    workflows/
      learn-from-reviews.yml   # Auto-learn from PR reviews
```

## After Setup

1. **Use it.** Start coding with your AI agent. Watch where it stumbles.
2. **Iterate.** When an agent makes a mistake, add one line to AGENTS.md that prevents it.
3. **Prune.** When a line stops being useful, delete it.
4. **Hand off.** Before ending long sessions, update HANDOFF.md.
5. **Review.** Check your configs every few weeks. Delete what's stale.

Your codebase gets smarter with every iteration.

## Verify

Run `/nv-context` again anytime to re-score your setup and find gaps.
