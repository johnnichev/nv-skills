# nv-context

Context engineering skill distribution. NOT an application -- this repo ships SKILL.md and supporting docs to `~/.claude/skills/nv-context/`.

## Commands

```bash
# Install skill globally (recommended)
npx skills add johnnichev/nv-context -g -y

# Install skill manually
mkdir -p ~/.claude/skills/nv-context && cp skills/nv-context/SKILL.md ~/.claude/skills/nv-context/

# Test skill works (open any project, then run)
/nv-context

# Verify SKILL.md line count (MUST stay under 500)
wc -l skills/nv-context/SKILL.md
```

## Stack

- Pure markdown skill -- no runtime, no dependencies, no build step
- `package.json` exists for npm discoverability only (no scripts, no node_modules)
- `hooks/` contains **reference examples** users copy into their own repos, not hooks for this repo

## Boundaries

### Always
- Run `wc -l skills/nv-context/SKILL.md` after any edit -- MUST be under 500 lines
- Validate that SKILL.md Phase 0 still offers ONE confirmation (not a form)
- Keep AGENTS.md under 200 lines, CLAUDE.md under 50 lines

### Ask First
- Changing the 8 Core Laws in SKILL.md (these are research-backed)
- Modifying the L0-L6 maturity criteria or Hierarchy of Leverage scoring rubric
- Adding new phases to SKILL.md (each phase costs ~30 lines of budget)
- Changing install commands in README.md or docs/QUICKSTART.md

### Never
- NEVER modify files in `research/logs/` -- these are completed research artifacts (484KB, 12 docs, 200+ sources)
- NEVER change the $1000 prompt scoring criteria referenced in research
- NEVER add runtime dependencies to package.json (this is a pure markdown skill)
- NEVER commit .private/ contents
- NEVER use `${{ }}` directly inside GitHub Actions `run:` blocks -- MUST use env vars to prevent script injection

## Landmines

- `skills/nv-context/SKILL.md` (477 lines): 23 lines from the 500-line hard cap. Every line added MUST justify removing another. The skill loads into agent context on every invocation -- bloat here costs tokens across every user's session.
- `skills/nv-context/*.template` files: These are OBSOLETE. SKILL.md v3 generates all content inline per the "Commands Beat Prose" law. Templates remain as reference examples only -- NEVER reference them from SKILL.md as `@imports`.
- `hooks/learn-from-reviews.yml` (line 21): Contains a **script injection vulnerability** -- `${{ github.event.review.body }}` is interpolated directly in a `run:` block. MUST use `env:` indirection instead. See SKILL.md Phase 7 for the correct pattern.
- `hooks/settings.json.template`: Placeholder commands `[FORMAT_COMMAND]`, `[LINT_COMMAND]`, `[TEST_COMMAND]` -- these are meant to be replaced per-project by the skill, not used as-is.
- `agents/` and `commands/` directories: Empty placeholders. Do not add files here without a design decision on the distribution model.
- `docs/QUICKSTART.md` (line 12,19): Install URLs reference `nv-skills` repo name but the actual repo is `nv-context`. MUST stay in sync with package.json `repository.url`.

## Patterns

```markdown
<!-- CORRECT: Positive instruction (research-backed) -->
MUST use date-fns for all date operations

<!-- WRONG: Negative instruction (increases likelihood of violation) -->
Don't use moment.js
```

```yaml
# CORRECT: GitHub Actions with env indirection (prevents script injection)
- name: Extract learning
  env:
    REVIEW_BODY: ${{ github.event.review.body }}
  run: |
    LEARNING=$(echo "$REVIEW_BODY" | sed 's/@claude-learn//' | xargs)

# WRONG: Direct interpolation in run block (script injection vector)
- name: Extract learning
  run: |
    LEARNING=$(echo "${{ github.event.review.body }}" | sed 's/@claude-learn//' | xargs)
```
