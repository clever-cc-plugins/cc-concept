---
name: cc-concept-campaign-concept
description: >
  Use this skill to build a complete campaign concept — goals, target audience, key
  messages, channel mix, and creative brief — from a campaign objective. Invoke when
  the user asks to "plan a campaign", "build a campaign concept", "create a campaign
  brief", or names a campaign type (e.g. "plan a product launch campaign"). Produces
  a campaign concept and offers to save it as brief.md for cc-content skills to
  consume.
allowed-tools: Read, Write, Edit, Bash
argument-hint: "[--type product-launch|thought-leadership|seasonal-promotion|retention|lead-generation|brand-awareness]"
---

# Campaign Concept Skill

This skill turns a campaign objective into a complete campaign concept, and hands the
result to `cc-content` as `brief.md`.

This skill follows the shared step sequence in `../_shared/skill-contract.md`. Steps
below add only campaign-concept-specific behavior.

## Step 0–1: Recall learnings and load context

If `.claude/learnings.md` exists, read it silently. Apply relevant entries — in
particular, campaign-type preferences, rejected frameworks, or discovered strategy
constraints. Do not announce this step. If the file is absent, continue normally.

Read the `## Context files` table in `CLAUDE.md`. Match the following needs against
the **Summary** column semantically — never against a label or filename:

- **Business goals/KPIs** — campaign objectives, business targets, success metrics,
  growth stage, revenue targets
- **Target audience** — positioning, audience profile, customer segments, buyer personas,
  organization background (prefer a `cc-concept-positioning` output file if registered)

Note silently if present (do not ask about): competitive landscape, current marketing
channels, growth stage, brand-specific strategy overrides.

## Step 2: Gating — Three-State Model

This skill gates on **exactly two** needs: **business goals** and **target audience**.
For each, resolve one of three states:

1. **Covered** — present in the context table (Summary match) → use silently, no ask.
2. **Absent-but-supplied** — ask **once** (never twice in one invocation); user
   answers → use, non-degraded.
3. **Absent-and-unanswered** — asked once, no usable answer → that section is
   labelled **⚠ DEGRADED**, never fabricated, and the rest of the campaign still
   generates.

### Check business goals

Search the context table Summary column for semantic matches: business goals, KPIs,
objectives, targets, growth stage, success metrics.

If **covered**, use silently.

If **absent**, ask once:

> "I need to understand what this campaign should achieve. Briefly: What are your
> primary business goals or KPIs right now? (e.g. revenue growth, lead volume,
> retention, brand awareness) Is there a specific target or metric this campaign
> should move?"

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

> "I need to understand who this campaign is for. Briefly: Who is the target
> audience? (role, company type/size if B2B, or demographic if B2C) What stage
> are they typically at when they encounter you? (just learning you exist, actively
> comparing options, or already a customer)"

If the user provides usable answers, proceed **non-degraded**. If the user declines
or the answer is too vague to use, label the section `## Target Audience ⚠ DEGRADED`
in the output and continue.

## Step 3: Calibrate

If `--type` was passed in `$ARGUMENTS`, use it directly and skip the campaign-type
question. Otherwise infer campaign type, funnel stage, and B2B/B2C from loaded
context; where inference isn't confident, ask the missing question directly rather
than guessing.

Present a one-line inference summary (e.g. `"Type: product launch · Audience: B2B
mid-market · Stage: TOFU"`) and wait for user confirmation or correction before
drafting.

## Step 4: Generate

Apply the three frameworks from `../_shared/campaign-frameworks.md` per that file's
facet mapping. **State the mapping being applied** before generating. Example:

> "Structuring with SOSTAC; sequencing channels with RACE (retention emphasis);
> messaging with Message House."

Produce a campaign concept that includes:

- **Campaign name** — memorable, descriptive working name for this initiative.
- **Campaign objective** — the specific outcome this campaign drives, tied to the
  loaded business goals.
- **Target audience summary** — the specific segment(s) this campaign addresses,
  reflecting positioning or organization context if available.
- **Key messages** — at least two key messages, each corresponding to a Message House
  pillar grounded in loaded context (positioning output, organization background,
  competitive landscape if available).
- **Channel mix** — proposed channels sequenced by RACE stage (Reach, Act, Convert,
  Engage) appropriate to the campaign type and funnel stage.
- **Creative brief** — tone/voice notes if brand-voice context is loaded, primary
  call-to-action, constraints (budget, timeline, resource availability), and suggested
  content formats per channel.

## Step 5: Internal quality check

Review the generated campaign concept for:

- **Completeness**: All six elements above are present (campaign name, objective,
  target audience, key messages, channel mix, creative brief).
- **Extractability**: The four `cc-content`-extractable elements (business goals, key
  messages, constraints, CTAs) are present in prose — this check is what Step 6.5
  relies on before offering to save to `brief.md`.
- **Framework alignment**: SOSTAC structures the campaign; RACE sequences the channels;
  Message House anchors the messaging.
- **Consistency**: All sections reinforce the same campaign positioning and objective.

Fix any gaps before proceeding.

## Step 6: Delimited output

Return the campaign concept inside clear delimiters:

```
─────────────────────────────────────────────────────────────────
## [Campaign Name]
─────────────────────────────────────────────────────────────────

[Generated campaign concept here]

─────────────────────────────────────────────────────────────────
```

## Step 6.5: Offer to save as brief.md

After showing the delimited output:

1. Check if `brief.md` exists in the working directory (the project root — not under
   `context/`). Run `ls brief.md` from `$PWD`.
2. If it exists: read it, extract the campaign name (or first heading) and the file's
   last-modified timestamp, and show both to the user. Ask: overwrite / save under a
   different name / cancel.
3. If the user chooses **save under a different name**: ask for a filename (or propose
   one derived from the new campaign name), write to that filename instead, and do not
   touch the existing `brief.md`.
4. If the user chooses **overwrite** or if no `brief.md` exists: write directly to
   `brief.md`.

**Do not** register `brief.md` in the `## Context files` table in `CLAUDE.md` — it is
a handoff artifact, not persistent context.

## Step 7: Feedback

Store learnings tagged `[cc-concept:cc-concept-campaign-concept]` in `.claude/learnings.md`.
Examples:

```
[cc-concept:cc-concept-campaign-concept] client rejected the inferred "lead-generation" type for a customer-only campaign; retention fits their base better — 2026-07-18
[cc-concept:cc-concept-campaign-concept] client prefers email + LinkedIn as primary channels, treats paid social as a last resort — 2026-07-18
```

If the session revealed a campaign-type preference, framework override, or project
constraint that future runs should apply, record it now.
