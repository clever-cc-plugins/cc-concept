---
name: cc-concept-content-strategy
description: >
  Use this skill to produce an editorial planning framework covering content pillars,
  topic clusters, content type mix, and publishing cadence. Invoke when the user asks
  for a "content strategy", "editorial plan", "content pillars", or "topic clusters".
  Produces a content strategy document and registers it as project context so
  cc-content skills can align individual pieces to it.
allowed-tools: Read, Write, Edit, Bash
argument-hint: "[optional: brief or focus for the content strategy]"
---

# Content Strategy Skill

This skill produces an editorial planning framework — content pillars, topic clusters, content mix, and cadence — and registers the output as project context so `cc-content` skills automatically align individual pieces to it.

This skill follows the shared step sequence in `../_shared/skill-contract.md`. Steps below add only content-strategy-specific behavior.

## Step 0–1: Recall learnings and load context

If `.claude/learnings.md` exists, read it silently. Apply relevant entries — in
particular, content strategy preferences, rejected frameworks, or discovered constraints.
Do not announce this step. If the file is absent, continue normally.

Read the `## Context files` table in `CLAUDE.md`. Match the following needs against
the **Summary** column semantically — never against a label or filename:

- **Business goals/KPIs** — business objectives, targets, success metrics, growth stage
- **Target audience** — positioning, audience profile, customer segments, buyer personas, organization background (prefer a `cc-concept-positioning` output file if registered)

Note silently if present, never ask about: brand voice, existing content inventory, competitive landscape.

## Step 2: Gating — Three-State Model

This skill gates on **exactly two** needs: **business goals** and **target audience**.
For each, resolve one of three states:

1. **Covered** — present in the context table (Summary match) → use silently, no ask.
2. **Absent-but-supplied** — ask **once** (never twice in one invocation); user
   answers → use, non-degraded.
3. **Absent-and-unanswered** — asked once, no usable answer → that section is
   labelled **⚠ DEGRADED**, never fabricated, and the rest of the document still
   generates.

### Check business goals

Search the context table Summary column for semantic matches: business goals, KPIs, objectives, targets, growth stage, success metrics.

If **covered**, use silently.

If **absent**, ask once:

> "I need to understand what this content strategy should support. Briefly: What are your primary business goals or KPIs right now? (e.g. revenue growth, lead volume, retention, brand awareness) Is there a specific target or metric this content strategy should move?"

If the user provides a usable answer, proceed **non-degraded**. If the user declines or the answer is too vague to use, label the section `## Business Goals ⚠ DEGRADED` in the output and continue.

### Check target audience

Search the context table Summary column for semantic matches: target audience, positioning, organization background, customer segments, buyer profile.

Prefer a `cc-concept-positioning` output file's Summary if one is registered; else fall back to organization background.

If **covered**, use silently.

If **absent**, ask once:

> "I need to understand who this content is for. Briefly: Who is the target audience? (role, company type/size if B2B, or demographic if B2C) What stage are they typically at when they encounter your content? (just learning you exist, actively comparing options, or already a customer)"

If the user provides a usable answer, proceed **non-degraded**. If the user declines or the answer is too vague to use, label the section `## Target Audience ⚠ DEGRADED` in the output and continue.

## Step 3: Calibrate

Infer funnel stage and audience type from loaded context. Present a one-line inference summary and wait for user confirmation or correction before drafting. Include this example format: `"Audience: B2B mid-market · Goal: lead generation · Funnel focus: MOFU"`.

## Step 4: Generate

Apply Message House from `../_shared/campaign-frameworks.md`. **State the choice before generating:**

> "Using Message House for content pillar architecture."

Produce a content strategy that includes:

- **Content pillars** — at least two, each a Message House pillar, each with supporting topic clusters.
- **Content type mix** — a recommended mix of content types (e.g. blog, video, social, case study) with rationale tied to the inferred funnel stage (TOFU skews video/social; BOFU skews case studies/comparisons).
- **Publishing cadence** — a suggested frequency per content type.

## Step 5–6: Quality check and delimited output

Review the generated content strategy for:

- **Completeness**: All three elements above are present (at least two pillars, each with topic clusters; content type mix; publishing cadence).
- **Consistency**: All sections reinforce the same strategic focus and business goals.
- **Clarity**: The pillars are defensible and grounded in context.

Fix any gaps before proceeding.

If Step 2 ended in a degraded state for one or both gated needs (business goals and/or target audience), prefix the output with:

`⚠ DEGRADED OUTPUT — generated without: <comma-separated list of unmet needs>`

For example, if target audience is degraded but business goals are not, prefix with:

`⚠ DEGRADED OUTPUT — generated without: target audience`

If both are degraded, prefix with:

`⚠ DEGRADED OUTPUT — generated without: business goals, target audience`

If neither need is degraded, omit the prefix.

Return the content strategy inside clear delimiters:

```
─────────────────────────────────────────────────────────────────
## Content Strategy
─────────────────────────────────────────────────────────────────

[Generated content strategy here]

─────────────────────────────────────────────────────────────────
```

## Step 6.5: Register output

Write the content strategy document to `context/content-strategy.md` by convention. **Apply collision-check logic**: if the file already exists, append a `-N` suffix before `.md` (try `-2`, then `-3`, etc.) until a filename that does not already exist is found. Never overwrite an existing file.

Confirm the file was created, then add a row to the `## Context files` table in `CLAUDE.md`. Use this format:

```markdown
| Content strategy | `context/content-strategy.md` | Content strategy: content pillars, topic clusters, content type mix, publishing cadence |
```

The Summary must explicitly name "content strategy," "pillars," and "topic clusters" — this wording is what makes the file legible to cc-content-blog-article and cc-content-linkedin-post's Summary-matching; it is functionally part of this requirement, not cosmetic (FR-062).

Do **not** hand-edit the **Key Config Files** table — the pre-commit hook owns that sync.

## Step 7: Feedback

Store learnings tagged `[cc-concept:cc-concept-content-strategy]` in `.claude/learnings.md`. Examples:

```
[cc-concept:cc-concept-content-strategy] client prefers thought-leadership pillars over product-led pillars, positions as an industry voice — 2026-07-19
[cc-concept:cc-concept-content-strategy] client publishes weekly on LinkedIn but only monthly long-form; cadence recommendations should respect that split — 2026-07-19
```

If the session revealed a content-strategy preference, framework override, or project constraint that future runs should apply, record it now.
