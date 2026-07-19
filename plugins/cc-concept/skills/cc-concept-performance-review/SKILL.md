---
name: cc-concept-performance-review
description: >
  Use this skill to review whether a strategic concept's bets actually played out —
  a positioning claim, a channel allocation, a content-strategy pillar mix, a GTM
  milestone, or a campaign's stated goals. Invoke when the user says "review our
  strategy performance", "did our positioning hold up", "how did the campaign
  perform against plan", "review the channel mix results", or "strategic performance
  review". Works from whatever performance data the owner pastes in — there is no
  analytics API integration. Do NOT use it to analyze how an individual content piece
  performed structurally or tonally — that is cc-content-performance-review's job, a
  different plugin's skill at the content-piece altitude, not the strategy altitude.
allowed-tools: Read, Write, Edit, Bash
argument-hint: "[optional: path to performance notes or KPI data]"
---

# Strategic Performance Review Skill

This skill closes the loop every other `cc-concept` skill's Step 7 (feedback) opens
but never resolves: whether the strategic bet a concept document made actually played
out once real-world results came in. It never regenerates a positioning document,
channel plan, content strategy, GTM plan, or campaign concept itself — that stays the
job of the skill that produced it. It names which bet held up and recommends the
specific adjustment to feed into that skill's next run.

This skill adapts `../_shared/skill-contract.md`'s 8-step sequence rather than
following it literally — Steps 1–2 below do more work than the contract's generic
description, because five structurally different artifact types (positioning,
channel mix, content strategy, GTM plan, campaign concept) must be normalized into
the same shape before any performance data is compared against them.

## Step 0: Recall learnings

If `.claude/learnings.md` exists, read it silently. Apply relevant entries — in
particular, prior review scope choices or promotion-target preferences. Do not
announce this step. If the file is absent, continue normally.

## Step 1: Load context and identify scope

Read the `## Context files` table in `CLAUDE.md`. List every registered concept-scope
document you find: positioning, channel plan, content strategy, GTM plan, campaign
brief — matching against each row's **Summary**, never its label or filename.

If the owner already named which concept(s) to review, use that. Otherwise ask once:

> "Which concept should I review — positioning, channel mix, content strategy, GTM
> plan, a campaign brief, or more than one? I found: <list of registered documents>."

If nothing is registered, say so and stop — there is no baseline to check performance
against:

> "I don't see any concept documents registered yet. Run one of the concept-generation
> skills first (e.g. `/cc-concept-positioning`, `/cc-concept-channel-advisor`) before
> reviewing its performance."

## Step 2: Extract the bets

For each document in scope, read it and extract its falsifiable bets in this uniform
shape:

```
Bet: <the specific claim>
Expected signal: <what result would look like if the bet is right>
Source: <document + section>
```

Apply per artifact type:

- **Positioning document** → one bet: the target segment + differentiation claim
  resonates.
- **Channel plan** → one bet per recommended channel: this allocation produces this
  outcome.
- **Content strategy** → one bet per pillar: this pillar performs per its stated
  role in the mix.
- **GTM plan** → one bet per milestone: this milestone is achievable on this
  timeline.
- **Campaign concept** → one bet per stated goal.

Present the full extracted list **before** moving to Step 3 — the owner can correct a
misread bet before any data gets compared against it.

## Step 3: Gather performance data

Ask for whatever the owner has against the extracted bets:

> "What actually happened? Paste whatever data you have — channel results, campaign
> KPIs vs. goals, pillar-level engagement, milestone status, or just your read on how
> it went."

If data only covers some of the extracted bets, proceed with what's available. Note
which bets remain unevaluated — never fabricate a verdict for a bet with no data.

## Step 4: Verdict per bet

For each bet with data, assign exactly one of: **Validated**, **Invalidated**,
**Inconclusive** — with the evidence cited. For each bet without data: **Unevaluated**.

**Never average verdicts across bets into one score.** A channel plan with three
validated channels and one invalidated one gets four separate verdicts, not a 75%.

For each Validated or Inconclusive bet, note "no change needed" or a minor refinement.
For each Invalidated bet, recommend re-running the specific upstream skill that
produced the document, naming the specific adjustment (e.g. "re-run
`/cc-concept-channel-advisor` with budget shifted away from Channel X" — not a
generic "reconsider this channel").

## Step 5: Internal quality check

Confirm every verdict traces to either the extracted bet (Step 2) or the pasted data
(Step 3) — no verdict should introduce a claim that wasn't stated in either. Fix any
gaps before proceeding.

## Step 6: Delimited output

```
─────────────────────────────────────────────────────────────────
Strategy performance review — <document(s) reviewed>
─────────────────────────────────────────────────────────────────

Bet: <claim>
Verdict: Validated | Invalidated | Inconclusive | Unevaluated
Evidence: <what the data showed>
Recommendation: <re-run `/cc-concept-<skill>` with <specific adjustment> | no change needed>

[repeat per bet]

─────────────────────────────────────────────────────────────────
```

## Register output

Write the review to `context/strategy-performance-review.md` by convention. Apply the
same collision-check logic as `cc-concept-positioning`'s Step 6:

1. Check if `context/strategy-performance-review.md` exists.
2. If it exists, generate a distinct filename by appending a `-N` suffix before `.md`
   (e.g. `context/strategy-performance-review-2.md`). Keep incrementing N until a
   filename that does NOT already exist is found. Never overwrite an existing review.
3. Write to the final, collision-checked filename.

Confirm the file was created, then add a row to the `## Context files` table in
`CLAUDE.md`:

```markdown
| Strategy performance review | `context/strategy-performance-review.md` | Verdicts on which positioning/channel/content-strategy/GTM bets were validated by real-world results |
```

The Summary must be semantic and describe what the file covers. Do **not** hand-edit
the **Key Config Files** table — the pre-commit hook owns that sync.

## Step 7: Feedback

Store learnings tagged `[cc-concept:cc-concept-performance-review]` in
`.claude/learnings.md`. Examples:

```
[cc-concept:cc-concept-performance-review] client always wants channel-level data even when campaign hit overall goal — 2026-07-19
[cc-concept:cc-concept-performance-review] positioning bets take 2+ quarters to show signal; flag short review windows as inconclusive — 2026-07-19
```

If the session revealed a review-scope preference, a recurring evidence gap, or a
project constraint that future reviews should apply, record it now.
