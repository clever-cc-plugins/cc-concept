---
name: cc-concept-competitive-research
description: >
  Use this skill to run a standalone competitive or market audit — independent of
  whether a positioning exercise is happening this session. Invoke when the user
  asks to "research our competitors", "run a competitive audit", "who are we up
  against", "find our market gaps", or when cc-concept-positioning, cc-concept-gtm,
  or cc-concept-channel-advisor reports a missing "competitive landscape" need.
  Produces context/competitive-landscape.md for any gated skill to consume.
allowed-tools: Read, Write, Edit, Bash, WebSearch, WebFetch
argument-hint: "[optional: comma-separated list of named competitors]"
---

# Competitive Research Skill

This skill produces a competitive landscape document — a structured audit of 2–4
named or inferred competitors covering messaging, positioning, content strategy,
and market gaps. It registers the output as project context for reuse by
cc-concept-positioning, cc-concept-gtm, cc-concept-channel-advisor,
cc-concept-content-strategy, and cc-content skills.

This skill follows the shared step sequence in `../_shared/skill-contract.md`. Steps
below add only competitive-research-specific behavior.

## Step 0: Recall learnings

If `.claude/learnings.md` exists, read it silently. Apply relevant entries — in
particular, prior competitor selections, frameworks tried, or market-specific
constraints. Do not announce this step. If the file is absent, continue normally.

## Step 1: Load context and identify competitors

Read the `## Context files` table in `CLAUDE.md`. If present, load
`context/organization-background.md` (or equivalent Summary match: organization,
company, business model, background, profile, mission, values, size, market
position, customer, constraints) — competitive teardowns are grounded in what
the organization actually does.

Ask once to identify 2–4 competitors:

- **If `$ARGUMENTS` includes competitor names** (e.g. `/cc-concept-competitive-research
Acme, BigCorp, StartupX`) → parse and use them directly; skip the question.
- **If organization background is loaded and names obvious candidates** (e.g.,
  "competes against Salesforce, HubSpot, Pipedrive") → confirm and use them.
- **Otherwise, ask once:**

  > "Name 2–4 of your main competitors or market alternatives. (You can list
  > companies, product categories, or delivery models — e.g. 'Salesforce, HubSpot,
  > custom-built solutions'.) I'll research their recent public content to audit
  > messaging, positioning, and market gaps."

- **If the user doesn't name any and org background yields no hints** → proceed with
  a light audit scope ("I'll work with what you've given me; if you add competitor
  names later, we can run this again").

## Step 2: Briefing check

Confirm the audit has at least one named competitor to research. If none are
named and no organization background exists, flag this as a non-degraded case
and offer to proceed anyway (ask: "Should I proceed with what you have, or would
you like to add competitor names now?").

## Step 3: Calibrate

Consult the brief in `$ARGUMENTS`, if present. Set audit depth and scope:

- **Narrow brief** (e.g., "focus on messaging only" or "compare social strategy")
  → scope the audit tightly to those dimensions.
- **Broad brief** (e.g., "full competitive landscape") → develop a complete teardown
  across all dimensions.
- **No brief** → develop a full competitive audit across all dimensions.

## Step 4: Generate

For each competitor (up to 4), conduct a structured teardown using the framework
from `docs/research/cc-concept-competitive-research.md` § 1 (repeatable
competitive-content teardown structure). The framework covers:

**A. Identity & positioning**

- Overview (company, target market, target audience)
- Positioning statement / category anchor
- Core value proposition
- Primary differentiator / "only-we" claim
- Positioning claims made (verbatim taglines/headlines)

**B. Messaging & voice**

- Messaging themes / pillars
- Tone & voice (formal/casual, technical/accessible)
- Consistency of voice across pages
- Emotional vs. rational appeal

**C. Target-segment signals**

- Personas addressed (job titles, industries)
- Segment-specific content/landing pages
- Buyer-committee roles targeted

**D. Content coverage & cadence**

- Topic clusters covered (breadth) and depth per cluster
- Format mix (blog, video, whitepaper, webinar, tools, interactive)
- Publishing frequency / cadence
- Content freshness
- Funnel-stage distribution (TOFU/MOFU/BOFU)

**E. Distribution & amplification**

- Social presence (platforms, follower counts, posting frequency, engagement rate)
- Backlink/referring-domain profile
- Earned media / press mentions

**F. Conversion architecture**

- Primary and secondary CTAs
- Lead-capture mechanisms
- Proof elements (case studies, testimonials, ROI calculators, comparison pages)

**G. Assessment**

- Standout/differentiating features
- Observed strengths and weaknesses
- Gap/opportunity notes

For each competitor, use `WebSearch` and `WebFetch` to pull recent public content
(site copy, blog archives, social feeds, press). Summarize findings per dimension
(score 1–5 or Harvey Ball notation where applicable). Flag standout strengths,
execution gaps, and underserved angles each competitor misses.

After the teardowns, synthesize a **content-focused SWOT per competitor** (3–4
items per quadrant), referencing only marketing/content/messaging factors:

- **Strengths** — dominant topic clusters, high-authority profile, consistent voice,
  clear differentiation.
- **Weaknesses** — thin topic coverage, stale content, weak messaging, missing
  funnel stages, format monotony.
- **Opportunities** — uncovered keywords/topics, underused formats, underserved
  segments, unaddressed trends.
- **Threats** — competitors with stronger resources, content easily replicated,
  rivals narrowing focus into your niche, algorithm/CTR changes.

**Share-of-Voice (SOV) sample.** Optionally include a light SOV estimate:

- **SEO SOV**: For 5–10 key category keywords (free via Google Keyword Planner),
  record each competitor's top 3 ranking positions and apply a documented CTR curve
  (position 1 ≈ 30%, position 2 ≈ 15%, position 3 ≈ 10%, etc.) to estimate search
  traffic share. Document your keyword set and CTR model.
- **Share of Search** (the most rigorous free proxy): Use Google Trends to compare
  search volume for each competitor's brand over the last 12 months. Record as a
  simple ratio (e.g., "3x more searches for Competitor A than Competitor B").

**Content-gap analysis.** Identify white space across competitors:

- Keywords or topics one or more competitors rank for that none of the others do.
- Content stages missing (commonly MOFU/BOFU — comparison pages, case studies,
  ROI calculators for specific verticals).
- Formats no competitor uses for a given topic (e.g., only long-form, no FAQ or
  video).
- Audience segments no competitor serves with dedicated content.

Prioritize gaps by impact (search volume, business relevance) and effort.

## Step 5: Internal quality check

Review the competitive landscape for:

- **Completeness**: All named competitors covered? All seven dimensions attempted?
- **Grounding**: Findings tied to actual public content, not speculation?
- **Consistency**: Scoring logic (1–5 or Harvey Balls) consistent across competitors?
- **Clarity**: Can someone unfamiliar with each company understand the summary?
- **Actionability**: Are gaps and opportunities concrete enough to feed positioning
  or content strategy work?

Fix any gaps before proceeding.

## Step 6: Delimited output

Return the competitive landscape inside clear delimiters:

```
─────────────────────────────────────────────────────────────────
## Competitive Landscape Audit
─────────────────────────────────────────────────────────────────

[Generated competitive landscape document here]

─────────────────────────────────────────────────────────────────
```

## Step 7: Register output

Write the competitive landscape document to `context/competitive-landscape.md` by
convention. **Apply collision-check logic** to ensure the file does not overwrite
or collide with an existing competitive analysis or market research file:

1. Check if `context/competitive-landscape.md` exists.
2. If it exists, generate a distinct filename by appending a `-N` suffix before
   `.md` (e.g., `context/competitive-landscape-2.md`). Keep incrementing N until
   a filename that does NOT already exist is found. Never overwrite an existing
   file.
3. Write to the final, collision-checked filename.

Confirm the file was created, then add a row to the `## Context files` table in
`CLAUDE.md` (or create the table if it does not exist). Use this format:

```markdown
| Competitive landscape | `context/competitive-landscape.md` | Competitive teardown, messaging audit, SWOT, share-of-voice, and content-gap analysis across 2–4 competitors; market gaps and underserved angles |
```

The Summary must include keywords "competitor", "competitive landscape", and
"market gap" so that gated skills (cc-concept-positioning, cc-concept-gtm,
cc-concept-channel-advisor) recognize and load it via semantic match — do not
hand-edit the **Key Config Files** table; the pre-commit hook owns that sync.

## Step 8: Feedback

Store learnings tagged `[cc-concept:cc-concept-competitive-research]` in
`.claude/learnings.md`. Examples:

```
[cc-concept:cc-concept-competitive-research] "share-of-voice" confuses clients; prefer "search visibility" — 2026-07-20
[cc-concept:cc-concept-competitive-research] industry leads with 5 key vendors, not 2-4; scope as broad audit when user lists >4 — 2026-07-20
```

If the session revealed a preferred competitor set, market dynamics, or a framework
that worked or didn't, record it now.
