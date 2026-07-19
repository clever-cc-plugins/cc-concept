# cc-concept HubSpot Gap Closure Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a new `cc-concept-performance-review` skill and extend `cc-concept-positioning` with an optional competitive content scan, closing the two `cc-concept`-side gaps found by comparing HubSpot's "Human+AI Content System" 20-prompt collection against the current skill set.

**Architecture:** One new Markdown skill file under `plugins/cc-concept/skills/`, one edited existing skill file (including an `allowed-tools` change to add live web research). No new `_shared/` files. No compiled code, no unit-test runner — "tests" are structural assertions (`python3` frontmatter parse, `grep` marker checks) plus manual fixture runs from the design doc (spec §5).

**Tech Stack:** Markdown (skill files), `prettier` (repo's PostToolUse formatter), `python3` (frontmatter/YAML validity checks), `gitleaks` (pre-commit secret scan).

## Global Constraints

- **Design source of truth:** `docs/superpowers/specs/2026-07-19-hubspot-gap-closure-design.md`. Every task traces to it.
- **Repo layout standard:** `marketplace/docs/cc-plugin-repo-guideline.md` — do not deviate.
- **Plugin name:** `cc-concept` (already scaffolded). Skills invoked by bare name, never namespaced.
- **No secrets** committed. **No `--force`** flags. Fix root causes.
- **Do not copy skill/plugin files between repos.**
- **`cc-concept-performance-review` adapts, not follows literally,** `_shared/skill-contract.md`'s 8-step sequence — Steps 1–2 do claim-extraction work the generic contract doesn't describe.
- **No analytics API integration** for `cc-concept-performance-review` — reasons only over owner-supplied data, same convention as `cc-content-performance-review` (the companion plugin's skill, a different altitude — content-piece patterns vs. strategic bets).
- **Per-bet verdicts, never averaged** — a document with 3 validated bets and 1 invalidated one gets 4 separate verdicts, not one aggregate score.
- **`cc-concept-positioning`'s competitive scan is optional, offered once, skippable** — declining leaves every existing step completely unchanged.
- **`allowed-tools` change:** `cc-concept-positioning` gains `WebSearch, WebFetch` — the only capability-surface expansion in this initiative; gated behind an explicit per-run opt-in, never automatic.
- **CLAUDE.md's Key Config Files table is never hand-edited** — the pre-commit `sync-config-table.sh` hook owns it. Pre-populate descriptions before committing so the hook doesn't write a `TODO` row.
- **Learnings tag:** `[cc-concept:cc-concept-performance-review]` — never write to another plugin's tag. `cc-concept-positioning`'s existing tag is unchanged.

---

## File Structure

| Path                                                               | Responsibility                                                                                           |
| ------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------- |
| `plugins/cc-concept/skills/cc-concept-performance-review/SKILL.md` | New skill: extract falsifiable bets from concept documents, verdict them against pasted performance data |
| `plugins/cc-concept/skills/cc-concept-positioning/SKILL.md`        | Edited: add Step 1.5 competitive content scan, `allowed-tools` gains `WebSearch, WebFetch`               |
| `CLAUDE.md`                                                        | +1 row in Key Config Files table (new skill); updated row for the edited skill                           |
| `README.md`                                                        | +1 row in the skill table                                                                                |

Already present, unmodified: `docs/superpowers/specs/2026-07-19-hubspot-gap-closure-design.md`, this plan file, `_shared/skill-contract.md`, `_shared/positioning-frameworks.md`, `_shared/campaign-frameworks.md`, all other existing skill files.

---

## Task 1: `cc-concept-performance-review` skill

Deliverable: a new skill that identifies which concept document(s) are in scope, extracts their falsifiable bets in a uniform shape, verdicts each against owner-supplied performance data, and recommends which upstream skill to re-run (spec §2).

**Files:**

- Create: `plugins/cc-concept/skills/cc-concept-performance-review/SKILL.md`
- Reference (read for shape, do not modify): `plugins/cc-concept/skills/_shared/skill-contract.md` (the 8-step sequence this skill adapts)
- Reference (read for shape, do not modify): `plugins/cc-concept/skills/cc-concept-positioning/SKILL.md` (Step 6's collision-check convention for registering output, to reuse verbatim)

**Interfaces:**

- Consumes: the `## Context files` table (to enumerate registered concept documents); pasted performance data or `$ARGUMENTS` file path.
- Produces: `context/strategy-performance-review.md` (collision-checked) and a `## Context files` row — read by any concept-generation skill's own Step 1 context load on a later run, via semantic Summary match. No other task in this plan consumes this directly.

- [ ] **Step 1: Write the SKILL.md frontmatter**

```markdown
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
```

- [ ] **Step 2: Write the skill body — intro and Steps 0–1**

```markdown
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
```

- [ ] **Step 3: Write the skill body — Steps 2–4 (extract bets, gather data, verdict)**

```markdown
## Step 2: Extract the bets

For each document in scope, read it and extract its falsifiable bets in this uniform
shape:

\`\`\`
Bet: <the specific claim>
Expected signal: <what result would look like if the bet is right>
Source: <document + section>
\`\`\`

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
```

- [ ] **Step 4: Write the skill body — Steps 5–6 (quality check, output, register)**

```markdown
## Step 5: Internal quality check

Confirm every verdict traces to either the extracted bet (Step 2) or the pasted data
(Step 3) — no verdict should introduce a claim that wasn't stated in either. Fix any
gaps before proceeding.

## Step 6: Delimited output

\`\`\`
─────────────────────────────────────────────────────────────────
Strategy performance review — <document(s) reviewed>
─────────────────────────────────────────────────────────────────

Bet: <claim>
Verdict: Validated | Invalidated | Inconclusive | Unevaluated
Evidence: <what the data showed>
Recommendation: <re-run `/cc-concept-<skill>` with <specific adjustment> | no change needed>

[repeat per bet]

─────────────────────────────────────────────────────────────────
\`\`\`

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

\`\`\`markdown
| Strategy performance review | `context/strategy-performance-review.md` | Verdicts on which positioning/channel/content-strategy/GTM bets were validated by real-world results |
\`\`\`

The Summary must be semantic and describe what the file covers. Do **not** hand-edit
the **Key Config Files** table — the pre-commit hook owns that sync.
```

- [ ] **Step 5: Write the skill body — Step 7 (feedback)**

```markdown
## Step 7: Feedback

Store learnings tagged `[cc-concept:cc-concept-performance-review]` in
`.claude/learnings.md`. Examples:

\`\`\`
[cc-concept:cc-concept-performance-review] client always wants channel-level data even when campaign hit overall goal — 2026-07-19
[cc-concept:cc-concept-performance-review] positioning bets take 2+ quarters to show signal; flag short review windows as inconclusive — 2026-07-19
\`\`\`

If the session revealed a review-scope preference, a recurring evidence gap, or a
project constraint that future reviews should apply, record it now.
```

- [ ] **Step 6: Verify frontmatter and key markers**

Run:

```bash
f=plugins/cc-concept/skills/cc-concept-performance-review/SKILL.md
python3 - "$f" <<'PY'
import sys, yaml
meta = yaml.safe_load(open(sys.argv[1]).read().split('---')[1])
assert meta['name'] == 'cc-concept-performance-review', meta.get('name')
assert 'allowed-tools' in meta
print("frontmatter OK")
PY
grep -q -i 'Expected signal' "$f" && grep -q -i 'Source:' "$f" && echo "bet shape OK"
grep -q -i 'never average verdicts' "$f" && echo "no-averaging constraint OK"
grep -q -i 'never fabricate a verdict' "$f" && echo "unevaluated constraint OK"
grep -q -i 'different plugin.s skill at the content-piece altitude' "$f" && echo "cc-content differentiation OK"
grep -q -i 'strategy-performance-review.md' "$f" && grep -q -i 'collision' "$f" && echo "registration OK"
grep -q -- '\[cc-concept:cc-concept-performance-review\]' "$f" && echo "learnings tag OK"
```

Expected: `frontmatter OK`, `bet shape OK`, `no-averaging constraint OK`,
`unevaluated constraint OK`, `cc-content differentiation OK`, `registration OK`,
`learnings tag OK`.

- [ ] **Step 7: Commit**

```bash
git add plugins/cc-concept/skills/cc-concept-performance-review/SKILL.md
git commit -m ":sparkles: feat(cc-concept): add strategic performance review skill"
```

---

## Task 2: `cc-concept-positioning` competitive content scan

Deliverable: `cc-concept-positioning` gains an optional, skippable Step 1.5 that
researches 2–4 named competitors' public content via `WebSearch`/`WebFetch`, feeding
its summary into the existing Step 2 competitive-landscape gate and Step 4 generation
(spec §3).

**Files:**

- Modify: `plugins/cc-concept/skills/cc-concept-positioning/SKILL.md`

**Interfaces:**

- Consumes: the existing skill's Step 2 gate and Step 4 framework generation.
- Produces: no other task depends on this.

- [ ] **Step 1: Update `allowed-tools` in the frontmatter**

Change line 9 from:

```
allowed-tools: Read, Write, Edit, Bash
```

to:

```
allowed-tools: Read, Write, Edit, Bash, WebSearch, WebFetch
```

- [ ] **Step 2: Insert Step 1.5 (competitive content scan)**

Insert this new section immediately after `## Step 1: Load context`'s existing
content (which ends after its two bullet points listing organization background and
competitive landscape needs) and before `## Step 2: Gating — Three-State Model`:

```markdown
## Step 1.5: Competitive content scan (optional)

Offer this once, before gating:

> "Want me to research your competitors' recent public content before we position
> against them? I can pull patterns in messaging and positioning from 2–4 competitors
> you name. This is optional — skip it and I'll rely on whatever competitive context
> you already have or supply directly."

- **Declined** → proceed straight to Step 2, unchanged.
- **Accepted** → ask the owner to name 2–4 competitors. For each, use `WebSearch` and
  `WebFetch` to pull recent public content (site copy, recent posts or announcements
  where reachable). Summarize per competitor: **messaging themes**, **stated or
  apparent differentiation**, **evident gaps or underserved angles**. Present this
  summary before continuing to Step 2.

This step never blocks either way — it is strictly additive research that, when it
succeeds, satisfies Step 2's competitive-landscape need (see Step 2 below) rather
than bypassing that gate.
```

- [ ] **Step 3: Update Step 2's competitive-landscape check to account for the scan**

Find the existing subsection `### Check competitive landscape` inside
`## Step 2: Gating — Three-State Model`. Immediately after its heading line, insert
this paragraph (before the existing "Search the context table Summary column..."
content):

```markdown
If Step 1.5's competitive content scan ran and produced a summary, treat that summary
as **covered** for this need — skip the direct question below entirely, since the
scan already supplies what it would have asked for. Only run the check below if Step
1.5 was declined or produced nothing usable.
```

- [ ] **Step 4: Update Step 4 (Generate) to use the scan's output**

Find the existing `## Step 4: Generate` section. Immediately after its heading line
and the "Select a positioning framework..." paragraph, insert this paragraph:

```markdown
If a competitive content scan summary is available (from Step 1.5 or supplied
directly by the owner), use it as the "competitive alternatives" input each framework
below already asks for — Obviously Awesome's alternatives list, Geoffrey Moore's
"differentiation" blank, the Perceptual Map's competitor plotting. This is richer
input into the same framework logic, not a change to the frameworks themselves.
```

- [ ] **Step 5: Verify the insertions**

Run:

```bash
f=plugins/cc-concept/skills/cc-concept-positioning/SKILL.md
grep -q 'WebSearch, WebFetch' "$f" && echo "allowed-tools updated"
grep -q '^## Step 1.5: Competitive content scan (optional)' "$f" && echo "Step 1.5 present"
grep -q 'strictly additive research' "$f" && echo "additive-not-bypass rule present"
grep -q 'treat that summary as \*\*covered\*\*' "$f" && echo "gate-satisfaction rule present"
grep -q 'richer input into the same framework logic' "$f" && echo "Step 4 usage rule present"
python3 - "$f" <<'PY'
import sys, yaml
meta = yaml.safe_load(open(sys.argv[1]).read().split('---')[1])
assert meta['name'] == 'cc-concept-positioning', meta.get('name')
assert 'WebSearch' in meta['allowed-tools'] and 'WebFetch' in meta['allowed-tools']
print("frontmatter OK")
PY
```

Expected: `allowed-tools updated`, `Step 1.5 present`, `additive-not-bypass rule
present`, `gate-satisfaction rule present`, `Step 4 usage rule present`,
`frontmatter OK`.

- [ ] **Step 6: Commit**

```bash
git add plugins/cc-concept/skills/cc-concept-positioning/SKILL.md
git commit -m ":sparkles: feat(cc-concept): add optional competitive content scan to positioning skill"
```

---

## Task 3: README and CLAUDE.md registration, fixture verification

Deliverable: the new skill is discoverable in `README.md`'s skill table and
registered in `CLAUDE.md`'s Key Config Files table with a real description (no `TODO`
placeholder); all seven fixtures from the design doc (spec §5) pass with the skills
invoked for real. This is the final task — no further tasks follow.

**Files:**

- Modify: `README.md` (skill table)
- Modify: `CLAUDE.md` (table row added by the pre-commit sync hook; pre-populate
  description before committing)

**Interfaces:**

- Consumes: the files committed in Tasks 1–2.

- [ ] **Step 1: Add the new skill to README.md's "At a glance" table**

Open `README.md`, find the table under `## At a glance`, and add a row after
`cc-concept-marketing-advisor` and before `cc-concept-learnings-promotion`:

```markdown
| `/cc-concept-performance-review` | Reviews whether a positioning, channel-mix, content-strategy, GTM, or campaign bet actually played out, and recommends the next adjustment |
```

- [ ] **Step 2: Pre-populate the CLAUDE.md row before the sync hook runs**

Open `CLAUDE.md`, find the `## Key Config Files` table, and add this row:

```markdown
| `plugins/cc-concept/skills/cc-concept-performance-review/SKILL.md` | Skill: Extract concept bets, verdict them against performance data, recommend re-runs |
```

Also update the existing `cc-concept-positioning` row's description to mention the
new capability:

```markdown
| `plugins/cc-concept/skills/cc-concept-positioning/SKILL.md` | Positioning skill: generates brand positioning from a selected framework; optional competitive content scan |
```

- [ ] **Step 3: Commit — verify no TODO rows remain**

```bash
git add README.md CLAUDE.md
git commit -m ":memo: docs(cc-concept): register strategic performance review and competitive scan"
grep -c 'TODO: add description' CLAUDE.md || echo "0 TODO rows OK"
```

Expected: the pre-commit hook's `sync-config-table` output reports either "no
changes" or an update that preserves your descriptions; `0 TODO rows OK` printed
after commit.

- [ ] **Step 4: Fixture A — scope identification across artifact types**

Manual, human-in-the-loop. Register both a positioning document and a channel-mix
recommendation in the context table. Run `/cc-concept-performance-review` without
naming a scope.
Expected: the skill lists both as available and asks which to review (or accepts
"both").
Fails if: the skill guesses a scope without asking, or misses a registered document.

- [ ] **Step 5: Fixture B — claim extraction produces per-channel bets**

Manual. With a channel plan recommending 3 channels in scope, run Step 2 of the
skill.
Expected: three distinct bets are extracted, one per channel, each with its own
expected signal — not one aggregate bet for the whole plan.
Fails if: the plan is treated as a single bet.

- [ ] **Step 6: Fixture C — partial data, partial verdicts**

Manual. Provide performance data covering only 2 of the 3 extracted bets from
Fixture B.
Expected: those two get a real verdict (validated/invalidated/inconclusive); the
third is marked **unevaluated**, never guessed.
Fails if: the skill fabricates a verdict for the bet with no data.

- [ ] **Step 7: Fixture D — recommendation names a specific upstream skill**

Manual. From Fixture C's invalidated bet.
Expected: the recommendation names `/cc-concept-channel-advisor` (or whichever skill
produced the invalidated document) with a specific adjustment — not a generic
"reconsider this channel."
Fails if: the recommendation is generic or names the wrong skill.

- [ ] **Step 8: Fixture E — registered review feeds a later run**

Manual. After Fixture D completes and `context/strategy-performance-review.md` is
registered, run `/cc-concept-channel-advisor` again.
Expected: the skill's context load picks up the performance review as relevant
context (semantic match on its Summary), and the regenerated channel mix reflects the
prior verdict.
Fails if: `cc-concept-channel-advisor` never loads or references the review.

- [ ] **Step 9: Fixture F — competitive scan is skippable and additive**

Manual. Run `/cc-concept-positioning` and decline the Step 1.5 offer.
Expected: behavior is identical to today's skill — Step 2's competitive-landscape
gate asks the owner directly if nothing is registered, exactly as before.
Fails if: declining changes any other step's behavior.

- [ ] **Step 10: Fixture G — competitive scan satisfies the existing gate**

Manual. Run `/cc-concept-positioning`, accept the Step 1.5 offer, name 2 competitors.
Expected: Step 2's competitive-landscape need is marked covered (no redundant direct
question to the owner), and Step 4's generated positioning references the scan's
identified gaps.
Fails if: the owner is asked the competitive-landscape question again after a
successful scan, or the generated positioning ignores the scan's findings.

- [ ] **Step 11: Record fixture results**

After running Steps 4–10, note pass/fail for each in the session summary. Any
failure is a defect in Task 1 or 2's skill file — fix there and re-run, do not paper
over in the plan. Once all seven fixtures pass, this plan is complete.

---
