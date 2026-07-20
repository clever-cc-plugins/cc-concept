---
name: cc-concept-orchestrator
description: >
  Use this skill when the user states a broad marketing goal without naming a
  specific skill — "help us launch this product", "we need to grow our LinkedIn
  presence", "reposition us against this new competitor" — and needs to know which
  order of cc-concept and cc-content skills to run, not a single deliverable.
  Recommends and sequences skills; never invokes them automatically. Defers to
  cc-concept-marketing-advisor for open-ended questions that aren't goal-shaped.
allowed-tools: Read
argument-hint: "[the business goal, in the user's own words]"
---

# Engagement-Type Orchestrator Skill

This skill matches a stated business goal to one of six engagement types, audits which parts of the marketing value chain are already covered, and produces a numbered sequencing plan — recommending the specific `cc-concept` and `cc-content` skills to run, in order, to reach that goal without redundant re-work.

**Key principle:** Different engagement types need different subsets of the value chain. A product launch requires all stages; an always-on content program skips formal GTM planning; a crisis response trades depth for speed. This skill's job is to map the goal to its required stages, then recommend only the skills that close the gaps.

**Critical distinction:** This skill _recommends_ skills by bare name (e.g. `/cc-concept-audience`, `/cc-content-linkedin-post`); it never invokes them directly. The user runs each named skill themselves, one at a time, in the suggested sequence.

---

## Step 0: Recall learnings

If `.claude/learnings.md` exists, read it silently, all plugin tags. Apply relevant entries (e.g., prior engagement-type preferences, market-specific overrides, or goal clarifications). Never announce.

---

## Step 1: Classify the goal

Ask once to name the stated business goal. If `$ARGUMENTS` contains a goal, use it directly; otherwise ask:

> "What's your marketing goal? (E.g. 'launch a new product', 'grow our LinkedIn presence', 'reposition against a new competitor', or a goal you describe in your own words.)"

Parse the goal against the six engagement types defined in `docs/research/cc-concept-orchestrator.md` § _Taxonomy of Engagement Types_:

1. **Product launch (go-to-market)** — introducing a new product or feature to a market; the offer is new or new to this market
2. **Brand repositioning** — deliberately changing how the brand is perceived; usually triggered by strategy shift, merger, or brand outgrowth
3. **Always-on content / growth program** — continuous, open-ended content program with no fixed end date; systematic throughput
4. **Campaign-specific push** — single, high-intensity, time-bound burst around one idea or offer
5. **Market expansion** — taking an existing product into a new segment, geography, or vertical
6. **Crisis / reactive response** — rapid response to an unplanned external event; dominant constraint is time

If the goal maps to exactly one type, use it. If it reasonably maps to two or more equally, ask once to disambiguate:

> "Your goal could fit [Type A] or [Type B]. Which is closer: [brief description of Type A] or [brief description of Type B]?"

---

## Step 2: Load and audit the context table

Read the `## Context files` table in `CLAUDE.md` (if it exists). Match each row against the registered artifacts — look for:

- **Audience/personas** — context files labeled `audience`, `persona`, `ICP`, or `buyer profile`
- **Competitive landscape** — context files labeled `competitive`, `market audit`, `competitor`, or `SWOT`
- **Positioning** — context files labeled `positioning`, `brand positioning`, or `messaging`
- **Campaign/GTM planning** — context files labeled `campaign concept`, `brief.md`, `campaign plan`, `GTM plan`, or `go-to-market`
- **Content strategy** — context files labeled `content strategy`, `editorial plan`, `content pillars`, or `topic clusters`
- **SEO/keyword research** — context files labeled `SEO`, `keywords`, `topic clusters`, or `keyword research`

For each artifact you find, note its Summary column (the one-line description) — that's what you'll cite in Step 6 when marking it "skip".

---

## Step 3: Determine required value-chain stages

Using the engagement type from Step 1, consult `docs/research/cc-concept-orchestrator.md` § _Stage-by-Stage Necessity Matrix_ (the table listing engagement types and which stages are Y/O/N). Identify which stages are **Y** (required) and **O** (optional but often valuable).

---

## Step 4: Map required stages to specific skills

For each **required** or **optional** stage, map it to the skill(s) that produce it:

| Value-chain stage             | Required skill(s)                                                                                                                | Notes                                                                                           |
| ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| **Audience/insight research** | `/cc-concept-audience`                                                                                                           | Produces `context/audience-personas.md`; gates many downstream skills                           |
| **Competitive research**      | `/cc-concept-competitive-research`                                                                                               | Produces `context/competitive-landscape.md`; required for positioning and GTM                   |
| **Positioning**               | `/cc-concept-positioning`                                                                                                        | Produces positioning statement and brand narrative; gates content strategy and campaign concept |
| **Campaign/GTM planning**     | `/cc-concept-gtm` (for product launch, market expansion, brand reposition) or `/cc-concept-campaign-concept` (for campaign push) | GTM produces a phased launch plan; campaign-concept produces a brief for cc-content             |
| **Content strategy**          | `/cc-concept-content-strategy`                                                                                                   | Produces editorial framework (pillars, topics, cadence); gates all cc-content creation skills   |
| **SEO/keyword research**      | `/cc-concept-seo-research`                                                                                                       | Optional but often feeds content strategy; produces validated topic clusters                    |
| **Content production**        | `/cc-content-linkedin-post`, `/cc-content-blog-article`, `/cc-content-text`, etc.                                                | Format-specific drafting skills; routed through `/cc-content-atomize` if multiple formats       |
| **Distribution**              | `/cc-content-atomize` (if multiple formats) or format-specific skills                                                            | Multi-format repurposing; keeps claims consistent across channels                               |
| **Measurement**               | `/cc-concept-performance-review` or `/cc-content-performance-review`                                                             | Strategic review (concept bets) vs. content-piece review (structural variants)                  |

---

## Step 5: Check skip conditions

For each required stage, check whether an artifact from Step 2 passes the skip test. Per `docs/research/cc-concept-orchestrator.md` § _Skip-Signals_:

- **Audience research:** Skip if personas/ICPs exist, are <6–12 months old, built from primary research (not assumption), and sales/support describe the same customer.
- **Competitive research:** Skip if a teardown exists, is <6 months old, covers the _same_ market you're addressing, and the category is stable.
- **Positioning:** Skip if a positioning statement exists, was validated with customers (not just approved internally), and sales actually use its language.
- **Content strategy:** Skip if a documented content plan exists and the content needs still fit it; redo if the plan is outdated or pillar mix has drifted.
- **SEO/keyword research:** Skip if keyword-validated topic clusters already exist and are recent; consider a refresh if the market is shifting.

---

## Step 6: Generate the numbered execution plan

Output a delimited block (using triple backticks or a clear visual boundary) containing a numbered sequence. For each skill, include:

1. **Skill name** (bare name, no `/`, e.g. `cc-concept-audience`)
2. **Why** (one-line rationale tied to the engagement type)
3. **Skip marker if applicable** (e.g., "SKIP — audience-personas.md already registered and <6 months old; sales confirms current usage")

If a required stage is missing and no skip test passed, name the skill unconditionally. Example:

```
Engagement type: Product launch
Goal: Launch a new software product to SMBs

1. cc-concept-audience — Required for new product: need to understand target SMB buyers, their pain points, and buying process. (Not skipped: no personas on file.)

2. cc-concept-competitive-research — Required for new product: must know who SMBs see as alternatives and how to differentiate. (Not skipped: no competitive landscape on file.)

3. cc-concept-positioning — Required for new product: new offer requires new or validated positioning. (Not skipped: no positioning document on file.)

4. cc-concept-gtm — Required for new product: structure launch phases, milestones, and go/no-go criteria. (Not skipped: no GTM plan on file.)

5. cc-concept-content-strategy — Required for new product: define content pillars and cadence that support launch messaging. (Not skipped: no content strategy on file.)

6. cc-concept-seo-research — Optional for launch: keyword research will validate pillar topics and improve organic discoverability post-launch. (Recommended but not required.)

7. cc-content-linkedin-post — Required for new product: create launch-announcement posts for SMB audience and early adopters on LinkedIn.

8. cc-content-blog-article — Required for new product: write thought leadership pieces explaining the product category and why SMBs should care.

9. cc-content-atomize — Recommended: if you want to repurpose launch messaging across multiple channels (LinkedIn, email, blog) while keeping claims identical.

10. cc-concept-performance-review — Recommended post-launch: once launch is live and first results are in, review whether GTM milestones held and positioning messaging resonated.
```

---

## Step 7: Offer to save learnings

At the end, ask once:

> "Should I save any learnings from this sequence (e.g., 'we always need SEO research for SMB campaigns' or 'we already validate positioning with customers') to `.claude/learnings.md`?"

If the user names a learning, append it with the tag `[cc-concept:cc-concept-orchestrator]` and today's date.

---

## Step 8: Close

Summarize the engagement type, required count, and next step:

> "Plan complete. You have [N] required steps and [M] optional/recommended steps. Run them in order; each skill will ask for context if it's missing and offer to register outputs so downstream skills can discover them."
