---
name: cc-concept-positioning
description: >
  Use this skill to develop or refine product/company positioning — how the offering is
  differentiated, for whom, against which alternatives. Invoke when the user asks to
  "work on positioning", "define our positioning", "write a positioning statement",
  "differentiate us from competitors", or "position the product". Produces a positioning
  document and registers it as project context.
allowed-tools: Read, Write, Edit, Bash
argument-hint: "[optional: brief or focus for the positioning work]"
---

# Positioning Skill

This skill produces a positioning document — the strategic frame that downstream
content executes against. It generates a formal positioning statement grounded in
your organization's background and competitive landscape, and registers the output
as project context for reuse by cc-concept and cc-content skills.

This skill follows the shared step sequence in `../_shared/skill-contract.md`. Steps
below add only positioning-specific behavior.

## Step 0: Recall learnings

If `.claude/learnings.md` exists, read it silently. Apply relevant entries — in
particular, positioning preferences, rejected frameworks, or discovered constraints.
Do not announce this step. If the file is absent, continue normally.

## Step 1: Load context

Read the `## Context files` table in `CLAUDE.md`. Match the following needs against
the **Summary** column semantically — never against a label or filename:

- **Organization background** — mission, values, size, market position, customer
  segments, constraints
- **Competitive landscape** — competitors, positioning, market gaps, differentiation
  opportunities

## Step 2: Gating — Three-State Model

This skill gates on **exactly two** needs: **organization background** and
**competitive landscape**. Audience, language, and format preferences are noted
silently if present and **never block**.

For each gated need, resolve one of three states:

1. **Covered** — present in the context table (Summary match) → use silently, no ask.
2. **Absent-but-supplied** — ask **once** (never twice in one invocation); user
   answers → use, non-degraded.
3. **Absent-and-unanswered** — asked once, no usable answer → that section is
   labelled **⚠ DEGRADED**, never fabricated, and the rest of the document still
   generates.

### Check organization background

Search the context table Summary column for semantic matches: organization, company,
business model, background, profile, mission, values, size, market position,
customer, constraints, team.

If **covered**, use silently.

If **absent**, ask once:

> "I need to understand your organization to position it well. Briefly: Who are you?
> (name, type, size) What do you do? (products/services, market) Who do you serve?
> (customer segments, use cases) Any constraints I should know? (budget, team, timeline)"

If the user provides usable answers, proceed **non-degraded**. If the user declines
or the answer is too vague to use, label the organization background section
**⚠ DEGRADED** in the output and continue. Example format: `## Organization Background ⚠ DEGRADED` followed by a brief note such as "Information not provided."

### Check competitive landscape

Search the context table Summary column for semantic matches: competitor, competitive,
competitive landscape, differentiation, market gap, positioning, competitive set,
pain points.

If **covered**, use silently.

If **absent**, ask once:

> "I need to understand your competitive context. Tell me: Who are your main
> competitors? (2–5 names + brief positioning) What are they doing well? Where are
> the market gaps or underserved needs? How do you want to differentiate?"

If the user provides usable answers, proceed **non-degraded**. If the user declines
or the answer is too vague to use, label the competitive landscape section
**⚠ DEGRADED** in the output and continue.

## Step 3: Calibrate

Consult the brief in `$ARGUMENTS`, if present. Set positioning depth and scope:

- **Narrow brief** (e.g., "focus on SMB segment" or "emphasize price leadership") →
  scope the positioning tightly.
- **Broad brief** (e.g., "comprehensive positioning") → develop full positioning
  across all segments and value dimensions.
- **No brief** → develop comprehensive positioning across primary segments.

## Step 4: Generate

Select a positioning framework from `../_shared/positioning-frameworks.md` following
that file's selection process. **State the choice before generating:**

> "Using the [framework name] because [one-sentence reason]."

Apply the framework systematically:

- If using **Obviously Awesome**: list competitive alternatives, audit unique
  strengths, extract unique attributes, identify best-fit segment, frame the position.
- If using **Geoffrey Moore's template**: fill each blank (target, need, category,
  benefit, differentiation) thoughtfully. Be specific on alternatives.
- If using **Value Proposition Canvas**: map customer jobs/pains/gains to product
  features/pain relievers/gain creators; highlight alignment and gaps.
- If using **Perceptual Map**: choose two differentiating axes, plot competitors and
  your product, identify white space.

Generate a positioning document (400–600 words) that includes:

- **Market position** — how you define the category you compete in and why.
- **Target customer** — the specific segment(s) you serve best.
- **Unique value** — what makes you different and why it matters to that customer.
- **Competitive differentiation** — how you stand against key alternatives.
- **Proof points** — 2–3 concrete reasons customers believe this positioning.

## Step 5: Internal quality check

Review the generated positioning for:

- **Clarity**: Can a colleague explain it in one sentence?
- **Defensibility**: Is it grounded in real product strengths or market gaps?
- **Specificity**: Does it avoid generic claims (e.g., "best-in-class")?
- **Consistency**: Do all sections reinforce the same core message?

Fix any gaps before proceeding.

## Step 6: Delimited output

Return the positioning document inside clear delimiters:

```
─────────────────────────────────────────────────────────────────
## [Organization Name] Positioning Document
─────────────────────────────────────────────────────────────────

[Generated positioning document here]

─────────────────────────────────────────────────────────────────
```

## Register output

Write the positioning document to `context/brand-positioning.md` by convention.
**Apply collision-check logic** to ensure the file does not overwrite or collide
with an organization-profile file or any existing positioning context:

1. Check if `context/brand-positioning.md` exists.
2. If it exists, generate a distinct filename by appending a `-N` suffix before
   `.md` (e.g., `context/brand-positioning-2.md`). Keep incrementing N (try -2, then -3, etc.) until a filename that does NOT already exist is found. Never overwrite an existing file.
3. Write to the final, collision-checked filename.

Confirm the file was created, then add a row to the `## Context files` table in
`CLAUDE.md`. Use this format:

```markdown
| Brand positioning | `context/brand-positioning.md` | Product positioning, target customer, unique value, and competitive differentiation |
```

The Summary must be semantic and describe what the file covers — use keywords so
future coverage checks will find it. Do **not** hand-edit the **Key Config Files**
table — the pre-commit hook owns that sync.

## Step 7: Feedback

Store learnings tagged `[cc-concept:cc-concept-positioning]` in `.claude/learnings.md`.
Examples:

```
[cc-concept:cc-concept-positioning] client prefers "differentiation" over "positioning" — 2026-07-17
[cc-concept:cc-concept-positioning] SMB segment values cost-of-ownership more than feature breadth — 2026-07-17
```

If the session revealed a rejected framework, positioning preference, or project
constraint that future runs should apply, record it now.
