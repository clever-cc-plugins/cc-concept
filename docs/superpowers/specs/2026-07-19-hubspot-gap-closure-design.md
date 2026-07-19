# cc-concept — Design: Closing Gaps Found in the HubSpot "Human+AI Content System" Prompt Collection

**Status:** Approved for implementation
**Date:** 2026-07-19
**Source:** Comparison of HubSpot x MATG's "The Human+AI Content System: 20 Prompts That
Multiply Creativity" against the current skill set of `cc-content` and `cc-concept`.
**Companion doc:** `cc-content/docs/superpowers/specs/2026-07-19-hubspot-gap-closure-design.md`
(the same initiative's `cc-content`-side changes — `cc-content-humanize`,
`cc-content-performance-review`, and a `cc-content-text` atomization extension).

---

## 1. Purpose and scope

The companion doc covers three `cc-content`-side gaps found by comparing HubSpot's
20-prompt collection against both plugins. Two further gaps land on the `cc-concept`
side instead, because they concern strategic concepts rather than finished content
pieces:

1. **Competitive Content Analysis & Mood Board Creator** (HubSpot IDEATION prompt) —
   no skill does competitor-content research to find gaps before generating a
   strategic frame. `cc-concept-positioning` is the natural home: it already reasons
   about "competitive landscape" as a gated need (Step 2), but today relies entirely
   on what the owner supplies manually.
2. **OPTIMIZATION stage, strategy-level slice** — `cc-content-performance-review`
   (companion doc) closes the content-piece-level half of this gap; this document
   closes the other half: whether a _strategic bet_ — a positioning claim, a channel
   allocation, a content pillar, a GTM milestone — actually played out. Every
   `cc-concept` skill's Step 7 (feedback) logs corrections but nothing ever closes
   the loop on whether the underlying strategy worked once real-world results come in.

**In scope:** one new skill, one extension to an existing skill.

```
plugins/cc-concept/skills/cc-concept-performance-review/SKILL.md   (new)
plugins/cc-concept/skills/cc-concept-positioning/SKILL.md          (edit: competitive scan)
```

**Out of scope:** any change to `cc-concept-channel-advisor`, `cc-concept-content-strategy`,
`cc-concept-campaign-concept`, or `cc-concept-gtm` beyond being _readable_ by the new
performance-review skill — no new generation logic added to any of them this round.

---

## 2. New skill — `cc-concept-performance-review`

### 2.1 Frontmatter

`name: cc-concept-performance-review`. Trigger phrases: "review our strategy
performance", "did our positioning hold up", "how did the campaign perform against
plan", "review the channel mix results", "strategic performance review".
`allowed-tools: Read, Write, Edit, Bash`. `argument-hint: "[optional: path to
performance notes or KPI data]"`.

### 2.2 Design decisions — handling heterogeneous concept artifacts

The central design problem this skill solves: `cc-concept` produces five structurally
different artifact types (a positioning statement, a channel-mix recommendation, a
content-strategy framework, a GTM plan, a campaign concept), and a single performance
review can't treat them identically. The resolution is a **claim-extraction layer**
that normalizes all five into the same shape before reasoning about them:

- Every concept document, regardless of type, states one or more **falsifiable
  bets** — a claim that real-world results can support or contradict. A positioning
  document bets that a segment + differentiation claim will resonate. A channel plan
  bets that a given allocation will produce a given outcome per channel. A content
  strategy bets that its pillar mix will perform per pillar. A GTM plan bets that its
  milestones are achievable on its stated timeline. A campaign concept bets on its
  stated goals across its channel mix.
- **Step 2 (Extract the bets)** is where this skill does that normalization: for
  whichever document(s) are in scope, pull out the specific bets in a uniform format
  (claim → expected signal → what would confirm or refute it) before touching any
  performance data. This keeps Steps 3–4 identical regardless of which artifact
  type(s) are under review.
- **No analytics API integration** — same convention as `cc-content-performance-review`:
  the owner pastes whatever data they have (channel-level results, campaign KPIs vs.
  stated goals, pillar-level engagement, milestone attainment, qualitative
  observations).
- **Output recommends which upstream skill to re-run, not a rewrite.** This skill
  never regenerates a positioning document or a channel plan itself — that stays the
  job of `cc-concept-positioning`/`cc-concept-channel-advisor`/etc. It names the bet
  that failed or succeeded and suggests the specific adjustment the owner should feed
  back into a re-run of the relevant skill.
- **Registers its output as context** (`context/strategy-performance-review.md`),
  following the same collision-check convention as `cc-concept-positioning`'s Step 6,
  so every future concept-generation skill run picks up prior verdicts automatically
  — this is what makes performance review compound "over time" rather than being a
  one-off report.

### 2.3 Step sequence

Adapts `_shared/skill-contract.md`'s 8-step sequence; Steps 1–2 do more work than the
contract's generic description because of the claim-extraction problem above.

**Step 0 — Recall learnings** (silent, per contract).

**Step 1 — Load context and identify scope.** Read the `## Context files` table.
List every registered concept-scope document (positioning, channel plan, content
strategy, GTM plan, campaign brief) found there. If the owner named which concept(s)
to review, use that. Otherwise ask once:

> "Which concept should I review — positioning, channel mix, content strategy, GTM
> plan, a campaign brief, or more than one? I found: <list of registered documents>."

If nothing is registered yet, say so and stop — there is no baseline to check
performance against.

**Step 2 — Extract the bets.** For each document in scope, read it and extract its
falsifiable bets in this uniform shape:

```
Bet: <the specific claim>
Expected signal: <what result would look like if the bet is right>
Source: <document + section>
```

A positioning document yields one bet (segment + differentiation resonates); a
channel plan yields one bet per recommended channel; a content strategy yields one
bet per pillar; a GTM plan yields one bet per milestone; a campaign concept yields
one bet per stated goal. Present this extracted list before moving on, so the owner
can correct a misread bet before data gets compared against it.

**Step 3 — Gather performance data.** Ask for whatever the owner has against the
extracted bets:

> "What actually happened? Paste whatever data you have — channel results, campaign
> KPIs vs. goals, pillar-level engagement, milestone status, or just your read on how
> it went."

If data only covers some of the extracted bets, proceed with what's available and
note which bets remain unevaluated (never fabricate a verdict for a bet with no data).

**Step 4 — Verdict per bet.** For each bet with data: **validated** / **invalidated**
/ **inconclusive**, with the evidence cited. For each bet without data: **unevaluated**.
Do not average verdicts across bets into one score — a channel plan with three
validated channels and one invalidated one gets four separate verdicts, not a 75%.

**Step 5 — Internal quality check.** Confirm every verdict traces to either the
extracted bet (Step 2) or the pasted data (Step 3) — no verdict introduces a claim
that wasn't in either.

**Step 6 — Delimited output.**

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

**Register output.** Write to `context/strategy-performance-review.md` using the same
collision-check convention as `cc-concept-positioning` Step 6 (append `-N` suffix
rather than overwrite an existing review). Add a row to the `## Context files` table:

```markdown
| Strategy performance review | `context/strategy-performance-review.md` | Verdicts on which positioning/channel/content-strategy/GTM bets were validated by real-world results |
```

**Step 7 — Feedback.** Standard two-phase pattern, tagged
`[cc-concept:cc-concept-performance-review]`.

---

## 3. Extension — `cc-concept-positioning` competitive content scan

### 3.1 Design decisions

- **Optional, offered once, skippable.** Inserted as a new **Step 1.5**, between the
  existing Step 1 (load context) and Step 2 (gating). Declining leaves the skill's
  existing behavior completely unchanged — the competitive-landscape gate in Step 2
  still works exactly as it does today (ask the owner directly if nothing is
  registered).
- **New tool permissions.** `allowed-tools` gains `WebSearch, WebFetch` — this is the
  one design decision in this pass that expands a skill's capability surface rather
  than only adding steps. Justified because HubSpot's source prompt is explicitly a
  live-research prompt ("analyze the competitive landscape"); doing this from the
  owner's own manual description (today's only option) is much lower-value than
  actual research. Gated behind an explicit opt-in per run, never automatic.
- **Feeds Step 2's existing gate, doesn't bypass it.** A successful scan **populates**
  the competitive-landscape need the existing Step 2 gate already checks for — after
  a scan, the "absent" branch simply won't trigger because the need is now covered
  (scan output is used the same as if the owner had supplied it directly). This is
  additive, not a parallel path.
- **Scope: 2–4 competitors, patterns not exhaustive research.** Matches HubSpot's
  source prompt's request for "3–5 competitors" scaled down slightly to keep the scan
  fast; asks the owner to name the competitors rather than guessing who they are.

### 3.2 Step sequence changes

**New Step 1.5 (after Step 1, before Step 2) — Competitive content scan (optional).**
Offer once:

> "Want me to research your competitors' recent public content before we position
> against them? I can pull patterns in messaging and positioning from 2–4 competitors
> you name. This is optional — skip it and I'll rely on whatever competitive context
> you already have or supply directly."

- **Declined** → proceed straight to Step 2, unchanged.
- **Accepted** → ask for 2–4 competitor names, then use `WebSearch`/`WebFetch` to pull
  each competitor's recent public content (site copy, recent posts/announcements where
  reachable). Summarize per competitor: **messaging themes**, **stated or apparent
  differentiation**, **evident gaps or underserved angles**. Present this summary
  before continuing to Step 2.
- Whether accepted or declined, this step never blocks — it's strictly additive
  research that feeds Step 2's existing competitive-landscape check.

**Step 2 (existing) — Gating.** No change to the mechanics. If Step 1.5 ran and
produced a summary, that summary now **satisfies** the competitive-landscape need
(covered, not absent) — the existing "ask once" branch for that need is skipped
because the need is no longer absent. If Step 1.5 was declined or produced nothing
usable, Step 2 behaves exactly as it does today.

**Step 4 (existing) — Generate.** If a competitive scan summary is available (from
Step 1.5 or from the owner directly), use it as the "competitive alternatives" input
each positioning framework already asks for (Obviously Awesome's alternatives list,
Geoffrey Moore's "differentiation" blank, the Perceptual Map's competitor plotting) —
no change to the framework logic itself, only richer input into it.

---

## 4. File layout and config updates

One new skill directory, one edited file:

```
plugins/cc-concept/skills/cc-concept-performance-review/SKILL.md   (new)
plugins/cc-concept/skills/cc-concept-positioning/SKILL.md          (edited)
```

`CLAUDE.md`'s **Key Config Files** table is not hand-edited — `scripts/sync-config-table.sh`
owns it via the pre-commit hook. `README.md`'s skill table gets the new skill added by
hand.

`cc-concept-positioning`'s frontmatter `allowed-tools` changes from
`Read, Write, Edit, Bash` to `Read, Write, Edit, Bash, WebSearch, WebFetch` — the only
`allowed-tools` change in this initiative. No new `_shared/` files needed for either
change (the performance-review skill's claim-extraction logic is specific enough to
this skill that it doesn't warrant a shared reference other skills would select from).
No marketplace.json changes — `plugins/cc-concept/` is already referenced via
`git-subdir` at the directory level.

---

## 5. Verification

Fixtures to run manually post-implementation:

**Fixture A — scope identification across artifact types.** Register both a
positioning document and a channel-mix recommendation in the context table. Run
`/cc-concept-performance-review` without naming a scope. Expected: the skill lists
both as available and asks which to review (or accepts "both").

**Fixture B — claim extraction produces per-channel bets.** With a channel plan
recommending 3 channels in scope, run Step 2. Expected: three distinct bets are
extracted, one per channel, each with its own expected signal — not one aggregate bet
for the whole plan.

**Fixture C — partial data, partial verdicts.** Provide performance data covering
only 2 of 3 extracted bets from Fixture B. Expected: those two get a real verdict
(validated/invalidated/inconclusive); the third is marked **unevaluated**, never
guessed.

**Fixture D — recommendation names a specific upstream skill.** From Fixture C's
invalidated bet, expected: the recommendation names `/cc-concept-channel-advisor`
(or whichever skill produced the invalidated document) with a specific adjustment —
not a generic "reconsider this channel."

**Fixture E — registered review feeds a later run.** After Fixture D completes and
`context/strategy-performance-review.md` is registered, run `/cc-concept-channel-advisor`
again. Expected: the skill's context load picks up the performance review as relevant
context (semantic match on its Summary), and the regenerated channel mix reflects the
prior verdict.

**Fixture F — competitive scan is skippable and additive.** Run
`/cc-concept-positioning` and decline the Step 1.5 offer. Expected: behavior is
identical to today's skill — Step 2's competitive-landscape gate asks the owner
directly if nothing is registered, exactly as before.

**Fixture G — competitive scan satisfies the existing gate.** Run
`/cc-concept-positioning`, accept the Step 1.5 offer, name 2 competitors. Expected:
Step 2's competitive-landscape need is marked covered (no redundant direct question to
the owner), and Step 4's generated positioning references the scan's identified gaps.

---

## 6. Traceability

| Gap (HubSpot prompt)                                                                                                           | Where addressed                         |
| ------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------- |
| Competitive Content Analysis & Mood Board Creator                                                                              | §3 (`cc-concept-positioning` extension) |
| Performance Pattern Recognition / Predictive Performance Modeler / Competitive Intelligence Integration (strategy-level slice) | §2 (`cc-concept-performance-review`)    |
