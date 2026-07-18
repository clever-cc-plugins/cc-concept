---
name: cc-concept-onboarding
description: >
  Use this skill to set up or extend the strategic context a marketing project needs
  before positioning, competitive, or go-to-market work. Invoke when the user asks to
  "onboard for strategy", "set up strategy context", "add competitive context", or when
  a cc-concept skill reports a missing strategic need. Runs standalone and also
  recognises context an existing cc-content project already provides.
allowed-tools: Read, Write, Edit, Bash
argument-hint: "[optional: path to an existing file to register as strategic context]"
---

# Onboarding Skill

This skill collects the strategic context downstream cc-concept skills need to run —
positioning, competitive analysis, go-to-market planning, and campaign concepting. Context
files are Markdown documents registered in the `## Context files` table of `CLAUDE.md`.
Skills load them on demand to set strategy accurately and at the right depth instead of
defaulting to generic frameworks. This skill runs standalone and also recognizes context
that an existing cc-content project already provides.

This skill follows the shared step sequence in `../_shared/skill-contract.md`. Steps below
add only onboarding-specific behavior. (Steps 5 and 6 from the contract are omitted because this skill collects multiple context files rather than emitting a single artifact.)

## Step 0: Recall learnings

If `.claude/learnings.md` exists, read it silently. Apply relevant entries — in particular,
path preferences, rejected interview answers, or project constraints discovered in prior runs.
Do not announce this step. If the file is absent, continue normally.

## Step 1: Discover existing context

This skill runs inside the owner's project — an arbitrary repo that may already have its own
structure, possibly with more than one `CLAUDE.md` at different levels (root plus nested ones
for sub-brands or campaigns). Never assume a single root-level file. Scan the whole project:

```bash
find . -name 'CLAUDE.md' -not -path '*/.git/*' -not -path '*/node_modules/*' | sort
find . -type d -iname 'context' -not -path '*/.git/*' -not -path '*/node_modules/*' | sort
```

For each `context/`-like folder found, list its files too — the `## Context files` table only
shows registered entries, and a folder can hold files nobody registered yet:

```bash
for d in <each context-like folder path from the find above>; do
  echo "=== $d ==="
  find "$d" -type f -name '*.md' | sort
done
```

For each `CLAUDE.md` found, check whether it already has a `## Context files` table:

```bash
for f in <each CLAUDE.md path from the find above>; do
  echo "=== $f ==="
  grep -A 200 '## Context files' "$f" 2>/dev/null || echo "(no context table)"
done
```

Keep the full list of discovered `CLAUDE.md` paths — Step 4 needs it to decide where each
newly registered file belongs. Show the owner the full picture, grouped by location:

> "Here's what your project already has set up:
>
> **Root** (`CLAUDE.md`)
>
> | Label                        | File | Summary |
> | ---------------------------- | ---- | ------- |
> | <existing rows, or "(none)"> |
>
> (and nested locations if found)"

## Step 2: Coverage check

For each gated need below, decide **covered / uncovered** by semantic match against the
Summary column of the context table — never against a label or filename. The two needs are
evaluated **independently** — one being covered does not exempt the other. Explicitly, if
the project already has organization background covered (typical in a cc-content project),
and competitive landscape uncovered (cc-content never collects that), then collect only
competitive landscape.

**Gated need: Organization background** — the organization's mission, values, size, market
position, customer segments, and constraints. Keywords in Summary: organization, company,
business model, background, profile, audience, market position, customer, constraints,
mission, values, team, size.

**Gated need: Competitive landscape** — the competitive set, key competitors and their
positioning, market gaps, differentiation opportunities, and customer pain points. Keywords
in Summary: competitor, competitive, competitive landscape, differentiation, market gap,
positioning, competitive set, pain points.

For each uncovered need, proceed to Step 3. If all needs are covered, there is nothing to collect or register; go to Step 7 (Feedback).

## Step 3: Collect

For each uncovered need, follow one of two paths:

**Path A: Register a passed-in file.** If `$ARGUMENTS` contains a file path, use that as the
starting point for this need. Read it, confirm it covers the need, and continue to collect any remaining uncovered needs. All collected files (passed-in and interviewed) are registered together in Step 4.

**Path B: Guided interview.** For each uncovered need, run a brief interview to collect
the information. After the interview, write the response to a file with a collision-checked
name. Apply this collision-check logic:

1. Propose a default filename by convention (e.g., `context/organization-background.md` for
   the organization need, `context/competitive-landscape.md` for the competitive need).
2. Check if a file at that path already exists.
3. If it exists, generate a distinct filename by appending a `-N` suffix before the `.md`
   extension (e.g., `context/competitive-landscape-2.md`). Keep incrementing N (try -2, then -3, etc.) until a filename that does NOT already exist is found. Never overwrite an existing context file.
4. Write to the final, collision-checked filename.

**Sample interview for organization background:**

- Who is this organization? (name, type, size)
- What does it do? (products, services, market)
- Who does it serve? (customer segments, use cases)
- What are the business constraints? (budget, team size, timeline, channels)

**Sample interview for competitive landscape:**

- Who are the main competitors? (2–5 names + brief positioning)
- What are they doing well?
- What are the market gaps or underserved customer needs?
- How does this organization want to differentiate?

## Step 4: Register

For each newly collected file, add a row to the `## Context files` table in the appropriate
`CLAUDE.md` (the root level, or the most specific nesting level that applies). Use this format:

```markdown
| Label                   | File                                 | Summary                                                         |
| ----------------------- | ------------------------------------ | --------------------------------------------------------------- |
| Organization background | `context/organization-background.md` | Company mission, values, size, market position, and constraints |
| Competitive landscape   | `context/competitive-landscape.md`   | Key competitors, market gaps, and differentiation opportunities |
```

The Summary column must be semantic and describe the need it covers — use keywords that
match the ones in Step 2 so future coverage checks will find it. Do **not** hand-edit the
**Key Config Files** table — the pre-commit hook owns that sync.

## Step 7: Feedback

Store learnings tagged `[cc-concept:cc-concept-onboarding]` in `.claude/learnings.md`. For
example:

```
[cc-concept:cc-concept-onboarding] client prefers "go-to-market plan" over "GTM strategy" — 2026-07-17
[cc-concept:cc-concept-onboarding] org-background file should ask about primary channels early — 2026-07-17
```

If the session revealed a rejected answer, path preference, or project constraint that future
runs should skip, record it now.
