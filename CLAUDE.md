# Claude-Specific: nv-context

@AGENTS.md
@docs/MANIFESTO.md
@docs/HIERARCHY-OF-LEVERAGE.md
@docs/FAQ.md

## Session Management

When context gets heavy (~40 messages or after exploring research/):
1. Update HANDOFF.md with current progress
2. `/clear`
3. Start fresh: "Read HANDOFF.md and continue where I left off"

This outperforms auto-compaction. At 60% context = safe. At 70% = precision drops. At 85% = hallucinations start. Compact proactively.

## Compounding Engineering

When you make a mistake a rule could have prevented:
1. Fix the mistake
2. Add one line to AGENTS.md that prevents it
3. The codebase gets smarter with every session

## Claude-Specific

- SKILL.md is the product. Treat every edit like editing a prompt worth $1000.
- Use `wc -l` after every SKILL.md edit. The 500-line budget is a hard constraint, not a guideline.
- Research logs are excluded via .claudeignore. Read research/SYNTHESIS.md for the distilled version.
