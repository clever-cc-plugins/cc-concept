---
name: cc-concept-channel-advisor
description: >
  Use this skill to recommend a channel mix and tactics for a specific marketing goal,
  audience, and budget context. Invoke when the user asks to "recommend a channel mix",
  "which channels should we use", or wants a channel strategy for a goal or campaign.
  Produces recommended primary and supporting channels, tactical recommendations, and
  flags prerequisites the user may be missing.
allowed-tools: Read, Write, Edit, Bash
argument-hint: "[optional: goal or campaign this recommendation is for]"
---

# Channel Advisor Skill

This skill recommends a channel mix and tactics for a specific goal, audience, and budget
context, sequenced against the RACE funnel model.

This skill follows the shared step sequence in `../_shared/skill-contract.md`. Steps below
add only channel-advisor-specific behavior.

## Step 0–1: Recall learnings and load context

If `.claude/learnings.md` exists, read it silently. Apply relevant entries — in particular,
channel preferences, constraints, or vetoed channels. Do not announce this step. If the file
is absent, continue normally.

Read the `## Context files` table in `CLAUDE.md`. Match the following needs against the
**Summary** column semantically — never against a label or filename:

- **Business goals/KPIs** — campaign objectives, business targets, success metrics, growth stage, revenue targets
- **Target audience** — positioning, audience profile, customer segments, buyer personas, organization background (prefer a `cc-concept-positioning` output file if registered)

Note silently if present (do not ask about): current marketing channels, budget, and a
prior strategy performance review (`cc-concept-performance-review` output) if registered —
factor validated/invalidated channel bets into the recommendation.

## Step 2: Gating — Three-State Model

This skill gates on **exactly two** needs: **business goals** and **target audience**.
For each, resolve one of three states:

1. **Covered** — present in the context table (Summary match) → use silently, no ask.
2. **Absent-but-supplied** — ask **once** (never twice in one invocation); user
   answers → use, non-degraded.
3. **Absent-and-unanswered** — asked once, no usable answer → that section is
   labelled **⚠ DEGRADED**, never fabricated, and the rest of the recommendation still
   generates.

### Check business goals

Search the context table Summary column for semantic matches: business goals, KPIs,
objectives, targets, growth stage, success metrics.

If **covered**, use silently.

If **absent**, ask once:

> "I need to understand what this channel recommendation should achieve. Briefly: What are your
> primary business goals or KPIs right now? (e.g. revenue growth, lead volume, retention, brand
> awareness) Is there a specific target or metric this recommendation should support?"

If the user provides usable answers, proceed **non-degraded**. If the user declines
or the answer is too vague to use, label the section `## Business Goals ⚠ DEGRADED`
in the output and continue.

### Check target audience

Search the context table Summary column for semantic matches: target audience,
positioning, organization background, customer segments, buyer profile.

Prefer a `cc-concept-positioning` output file's Summary if one is registered; else
fall back to organization background.

If **covered**, use silently.

If **absent**, ask once:

> "I need to understand who this channel recommendation is for. Briefly: Who is the target
> audience? (role, company type/size if B2B, or demographic if B2C) What stage are they
> typically at when they encounter you? (just learning you exist, actively comparing options,
> or already a customer)"

If the user provides usable answers, proceed **non-degraded**. If the user declines
or the answer is too vague to use, label the section `## Target Audience ⚠ DEGRADED`
in the output and continue.

## Step 3: Calibrate

Take the goal from `$ARGUMENTS` if given, else from loaded business goals or the Step 2
gating answer. No campaign-type inference is needed here — just goal, audience, and
whatever current-channel/budget context is loaded.

## Step 4: Generate

Apply RACE from `../_shared/campaign-frameworks.md`. **State the mapping being applied**
before generating. Example:

> "Using RACE to sequence channels by funnel stage."

Produce a channel recommendation that includes:

- **Primary channel(s)** — with rationale tied to the loaded goal and audience.
- **Supporting channel(s)** — channels that reinforce the primary channel(s).
- **Tactical recommendations** — at least one concrete tactic per recommended channel.
- **Existing-channel calls** — for each existing channel loaded from context, a maintain/grow/reduce/exit call, based on whether the advisor is recommending continued/increased investment (maintain/grow), reduced investment (reduce), or discontinuing it (exit) — including channels the advisor is NOT recommending going forward. Omit this element entirely if no current-channels context is loaded.
- **Prerequisites** — for any recommended channel where the loaded context suggests it may be out of reach (budget, capability, or skills the user may not have), a "prerequisites" note naming what's missing.

## Step 5–6: Quality check and delimited output

Review the generated channel recommendation for:

- **Completeness**: All five elements above are present (existing-channel calls only when current-channels context was loaded).
- **Extractability**: Primary channels, supporting channels, and tactical recommendations are explicitly named so the user can act on them immediately.
- **Framework alignment**: RACE stages are clearly sequenced in the recommendation.
- **Consistency**: All sections reinforce the same goal and audience.

Fix any gaps before proceeding.

If Step 2 ended in a degraded state for one or both gated needs (business goals and/or
target audience), prefix the output with:

```
⚠ DEGRADED OUTPUT — generated without: <comma-separated list of unmet needs>
```

For example, if target audience is degraded but business goals are not, prefix with:
`⚠ DEGRADED OUTPUT — generated without: target audience`

If both are degraded, prefix with:
`⚠ DEGRADED OUTPUT — generated without: business goals, target audience`

If neither need is degraded, omit the prefix.

Return the channel recommendation inside clear delimiters:

```
─────────────────────────────────────────────────────────────────
## Channel Recommendation
─────────────────────────────────────────────────────────────────

[Generated channel recommendation here]

─────────────────────────────────────────────────────────────────
```

## Step 7: Feedback

Store learnings tagged `[cc-concept:cc-concept-channel-advisor]` in `.claude/learnings.md`.
Examples:

```
[cc-concept:cc-concept-channel-advisor] client vetoed paid social entirely, treat as excluded from all future recommendations — 2026-07-19
[cc-concept:cc-concept-channel-advisor] client's existing email list is small (<500) and shouldn't be weighted as a primary channel yet — 2026-07-19
```

If the session revealed a channel preference, constraint, or exclusion that future runs
should apply, record it now.
