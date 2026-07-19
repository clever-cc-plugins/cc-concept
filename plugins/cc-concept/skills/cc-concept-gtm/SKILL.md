---
name: cc-concept-gtm
description: >
  Use this skill to structure a go-to-market launch plan for a new product, service,
  feature, or market entry — audience, positioning, channel sequence, key messages, and
  milestones. Invoke when the user asks to "plan a launch", "go-to-market plan", "GTM
  plan", or names a launch type (e.g. "plan a feature release"). Produces a GTM plan and
  offers to save a brief.md-compatible campaign brief as a by-product.
allowed-tools: Read, Write, Edit, Bash
argument-hint: "[--type product-launch|feature-release|market-expansion]"
---

# Go-to-Market Skill

This skill structures a launch plan for a new product, service, feature, or market entry, and
optionally hands off a `brief.md`-compatible campaign brief as a by-product.

This skill follows the shared step sequence in `../_shared/skill-contract.md`. Steps below add
only GTM-specific behavior.

## Step 0–1: Recall learnings and load context

If `.claude/learnings.md` exists, read it silently. Apply relevant entries — in particular,
launch-type preferences, rejected frameworks, or discovered strategy constraints. Do not
announce this step. If the file is absent, continue normally.

Read the `## Context files` table in `CLAUDE.md`. Match the following needs against the
**Summary** column semantically — never against a label or filename:

- **Business goals/KPIs** — launch objectives, business targets, success metrics, growth
  stage, revenue targets
- **Target audience** — positioning, audience profile, customer segments, buyer personas,
  organization background (prefer a `cc-concept-positioning` output file if registered)

Note silently if present (do not ask about): competitive landscape, current marketing channels,
existing positioning depth, and a prior strategy performance review (`cc-concept-performance-review`
output) if registered — factor validated/invalidated milestone bets into the plan.

## Step 2: Gating — Three-State Model

This skill gates on **exactly two** needs: **business goals** and **target audience**. For each,
resolve one of three states:

1. **Covered** — present in the context table (Summary match) → use silently, no ask.
2. **Absent-but-supplied** — ask **once** (never twice in one invocation); user answers → use,
   non-degraded.
3. **Absent-and-unanswered** — asked once, no usable answer → that section is labelled
   **⚠ DEGRADED**, never fabricated, and the rest of the GTM plan still generates.

### Check business goals

Search the context table Summary column for semantic matches: business goals, KPIs, objectives,
targets, growth stage, success metrics.

If **covered**, use silently.

If **absent**, ask once:

> "I need to understand what this launch should achieve. Briefly: What are your primary business
> goals or KPIs for this launch? (e.g. revenue growth, lead volume, market share, brand awareness)
> Is there a specific target or metric this launch should move?"

If the user provides usable answers, proceed **non-degraded**. If the user declines or the answer
is too vague to use, label the section `## Business Goals ⚠ DEGRADED` in the output and continue.

### Check target audience

Search the context table Summary column for semantic matches: target audience, positioning,
organization background, customer segments, buyer profile.

Prefer a `cc-concept-positioning` output file's Summary if one is registered; else fall back to
organization background.

If **covered**, use silently.

If **absent**, ask once:

> "I need to understand who this launch is for. Briefly: Who is the target audience? (role,
> company type/size if B2B, or demographic if B2C) What stage are they typically at when they
> encounter this launch? (just learning you exist, actively comparing options, or already a
> customer)"

If the user provides usable answers, proceed **non-degraded**. If the user declines or the answer
is too vague to use, label the section `## Target Audience ⚠ DEGRADED` in the output and continue.

## Step 3: Calibrate

If `--type` was passed in `$ARGUMENTS`, use it directly and skip the launch-type question.
Otherwise infer the launch type from loaded context; where inference isn't confident, ask
directly rather than guessing. Present a one-line inference summary and wait for user
confirmation or correction before drafting.

- **product-launch** — full-depth treatment across all output elements.
- **feature-release** — lighter treatment; assumes existing audience and positioning are already
  known, focuses on messaging and milestones.
- **market-expansion** — emphasizes audience redefinition and channel sequencing for the new
  market.

## Step 4: Generate

Apply SOSTAC, RACE, and Message House from `../_shared/campaign-frameworks.md` per that file's
facet mapping. **State the mapping being applied** before generating. Example:

> "Structuring with SOSTAC; sequencing channels with RACE; messaging with Message House."

Produce a GTM plan that includes:

- **Target audience definition** — the specific segment(s) this launch addresses.
- **Positioning statement for the launch** — derived from loaded positioning context if present;
  otherwise generated fresh by following the selection process in
  `../_shared/positioning-frameworks.md`.
- **Channel sequence with timing** — proposed channels sequenced by RACE stage, with a rough
  timeline.
- **Key messages** — Message House pillars grounded in loaded context.
- **Launch milestones** — at least three, tied to the Control facet of SOSTAC.

## Step 5–6: Quality check and delimited output

Review the generated GTM plan for:

- **Completeness**: All five elements above are present (target audience definition, positioning
  statement, channel sequence with timing, key messages, launch milestones).
- **Milestone count**: At least three milestones are listed.
- **Framework alignment**: SOSTAC structures the plan; RACE sequences the channels; Message House
  anchors the messaging.
- **Consistency**: All sections reinforce the same launch positioning and objective.

Fix any gaps before proceeding.

If Step 2 ended in a degraded state for one or both gated needs (business goals and/or target
audience), prefix the output with:

```
⚠ DEGRADED OUTPUT — generated without: <comma-separated list of unmet needs>
```

For example, if target audience is degraded but business goals are not, prefix with:
`⚠ DEGRADED OUTPUT — generated without: target audience`

If both are degraded, prefix with:
`⚠ DEGRADED OUTPUT — generated without: business goals, target audience`

If neither need is degraded, omit the prefix.

Return the GTM plan inside clear delimiters:

```
─────────────────────────────────────────────────────────────────
## Go-to-Market Plan: [Launch Name]
─────────────────────────────────────────────────────────────────

[Generated GTM plan here]

─────────────────────────────────────────────────────────────────
```

## Step 6.5: Offer to save as brief.md

This is a Could-priority by-product (FR-072) — the GTM plan's key messages and channel mix,
packaged the same way cc-concept-campaign-concept packages a campaign brief.

After showing the delimited output:

1. Check if `brief.md` exists in the working directory (the project root — not under `context/`).
   Run `ls brief.md` from `$PWD`.
2. If it exists: read it, extract the campaign name (or first heading) and the file's
   last-modified timestamp, and show both to the user. Ask: overwrite / save under a different
   name / cancel.
3. If the user chooses **save under a different name**: ask for a filename (or propose one
   derived from the launch name), write to that filename instead, and do not touch the existing
   `brief.md`.
4. If the user chooses **overwrite** or if no `brief.md` exists: write directly to `brief.md`,
   covering the launch's key messages and channel mix.

Do **not** register brief.md in the ## Context files table in CLAUDE.md — it is a handoff
artifact, not persistent context, the same rule cc-concept-campaign-concept follows.

## Step 7: Feedback

Store learnings tagged `[cc-concept:cc-concept-gtm]` in `.claude/learnings.md`. Examples:

```
[cc-concept:cc-concept-gtm] client's feature-release launches skip the audience-redefinition step entirely, existing segments always apply — 2026-07-19
[cc-concept:cc-concept-gtm] client wants milestone dates expressed as week-of-launch offsets (T-4, T-2, T0) rather than calendar dates — 2026-07-19
```

If the session revealed a launch-type preference, framework override, or project constraint that
future runs should apply, record it now.
