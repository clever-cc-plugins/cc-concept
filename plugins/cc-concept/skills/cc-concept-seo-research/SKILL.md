---
name: cc-concept-seo-research
description: >
  Use this skill to build keyword-validated topic clusters for content planning.
  Invoke when the user asks to "research keywords", "find SEO topics", "what should
  we write about" backed by search demand, or when cc-concept-content-strategy is
  about to generate pillars without any keyword data loaded. Uses the Ubersuggest
  MCP tools when connected; falls back to an interview-based topic-gathering workflow
  when they are not available — never blocks on their absence.
allowed-tools: Read, Write, Edit, Bash
argument-hint: "[optional: seed topic or list of seed keywords]"
---

# SEO Research & Topic-Cluster Skill

This skill builds keyword-validated topic clusters, using professional SEO tools when available and gracefully degrading to interview-driven research when they are not. Topic clusters feed `cc-concept-content-strategy`'s pillar generation with actual search-demand signals.

Adapts `../_shared/skill-contract.md`'s 8-step sequence. Step 1 includes MCP detection; Step 4 branches into tool-assisted or fallback workflow per the research in `docs/research/cc-concept-seo-research.md`.

## Step 0: Recall learnings

If `.claude/learnings.md` exists, read it silently, across all plugin tags. Apply
relevant entries — in particular, preferred seed topics, rejected frameworks, or
discovered keyword patterns. Never announce this step; surface nothing unless it
changes behavior.

## Step 1: Load context and detect SEO tooling

Read the `## Context files` table in `CLAUDE.md`. Match the following needs against
the **Summary** column semantically:

- **Organization background** — business, market position, target offer
- **Target audience** — personas, customer segments, positioning

Note silently if present; never ask. If `cc-concept-positioning` output is registered,
prefer its Summary over organization background.

### MCP Tool Availability Detection

This skill works best with Ubersuggest MCP tools, but **never blocks on their absence**.

Attempt to detect whether any Ubersuggest-family MCP tool is available in this session
by checking your current system reminders for tool names matching the pattern
`*Ubersuggest*keyword_suggestions` or similar (e.g.,
`mcp__claude_ai_Ubersuggest__keyword_suggestions`). These tool names appear in your
system reminders if the MCP server is connected.

**If Ubersuggest tools are detected:** Proceed to the tool-assisted workflow
(Step 4a below). Do not announce detection; proceed silently.

**If Ubersuggest tools are not detected:** State once:

> "SEO tooling isn't connected this session — continuing with interview-based topic gathering"

Then proceed to the fallback workflow (Step 4b below). Do not treat this as a failure
or block. This is the skill's designed degrade path, same as `cc-content-blog-article`'s
fallback when brand voice is unavailable.

## Step 2: Briefing check — gated needs

This skill gates on **zero required needs** (like `cc-concept-audience`). Organization background and target audience improve the output but do not block it; the skill works standalone.

If organization background or target audience are already loaded (Step 1), use them
silently. If neither is present, proceed — the skill will ask one clarifying question
per workflow (tool-assisted: seed keywords; fallback: core business questions).

## Step 3: Calibrate

Ask once to establish the scope:

- **If tool-assisted:** "What is your core topic or primary seed keyword(s) for this
  research?" Record the answer.
- **If fallback:** "Briefly: What does your business do, and what core questions or
  pain points do your customers ask about most?" Record the answer.

## Step 4a: Generate — Tool-Assisted Workflow

If Ubersuggest (or other keyword tool) MCP tools are available, run this workflow.

Based on `docs/research/cc-concept-seo-research.md` §1 (Tool-Assisted Workflow):

1. **Seed expansion:** Take the seed keyword(s) from Step 3 and use an available
   Ubersuggest-family tool (e.g., `keyword_suggestions`, `keyword_ideas`) to expand
   into a comprehensive list of related keywords, long-tail variations, and question
   variations.

2. **Data collection:** For each expanded keyword, pull (where available):
   - **Search volume** — estimated monthly searches
   - **Keyword difficulty (or competition score)** — a 0–100 estimate of ranking
     competitiveness
   - **SERP features** — detected featured snippets, People Also Ask boxes, video
     packs, image packs, etc.
   - **Search intent** — classify as informational, commercial, or transactional

3. **Parent-topic clustering:** Use the tool's clustering feature (e.g., Ahrefs'
   "Parent Topic," Semrush's keyword clusters) or manually group keywords by SERP
   similarity: if the same top-ranking pages appear for two keywords, they belong in
   the same cluster.

4. **Content-gap analysis:** If the tool offers it, run a gap analysis against
   competitor domains (if available) to identify high-opportunity keywords competitors
   rank for but your business does not.

5. **Prioritization:** Score candidate clusters by:
   - Aggregate search volume across the cluster (prefer 500+ monthly searches combined)
   - Average keyword difficulty relative to site authority (new sites: KD <30; mature
     sites: KD <60)
   - Strategic relevance to the business (does the topic fit what you sell/stand for?)

6. **Cluster structure:** For each prioritized cluster, define:
   - **Pillar topic** — the broad, high-volume keyword at the cluster's center
   - **Cluster keywords** — 6–12 supporting long-tail variations with distinct intents
   - **Rationale** — search volume, difficulty, SERP features present, and strategic
     fit

Proceed to Step 5 with the tool-assisted cluster table.

## Step 4b: Generate — Fallback Workflow (No Tool)

If Ubersuggest or other keyword tools are not available, run this three-track manual
workflow. Based on `docs/research/cc-concept-seo-research.md` §3 (No-Tool Fallback Workflow):

### Track A — Competitor-Content Keyword Inference

1. **Assemble the competitor set:** Identify 3–5 direct competitors and/or SERP
   competitors (high-ranking publishers/review sites) in your space.

2. **Harvest on-page targets:** For each competitor, note:
   - Page titles (state the primary target keyword)
   - H1 and main subheadings (H2/H3) — these reveal subtopics and variations
   - Meta descriptions (often contain target phrases)

3. **Map recurring topics:** Build a spreadsheet of all unique subheading/section terms
   across competitors. Topics appearing on multiple competitors are validated (proof
   of market investment); topics only one covers may be gaps.

### Track B — Manual SERP-Signal Harvesting

4. **Autocomplete (ABC technique):** Type your core topic into Google and record
   predictions. Then append each letter a–z ("topic a," "topic b," "topic c," etc.)
   and common prepositions ("topic for," "topic with," "topic vs") to surface long-tail
   variations. Repeat on YouTube and Bing for platform-specific angles.

5. **People Also Ask (PAA):** Search your core topic in Google and record every
   question in the PAA box. Click each to expand and load related questions. Log
   verbatim; these are the exact questions to answer. Recurring questions across
   multiple seed searches are high-signal.

6. **Related searches:** Scroll to the bottom of each Google results page and record
   "Related searches." Pick the most relevant, search them, and record _their_ related
   searches recursively. Stop when ideas repeat.

7. **Forums and Q&A communities:** Search your topic on Reddit and Quora, filtering
   for high upvotes/engagement. Record exact customer language, recurring pain points,
   and most-asked questions. Niche forums are goldmines for real market language.

### Track C — SME Interview / Internal Elicitation

8. **Interview customer-facing staff** (sales, support, success) or domain experts:
   - What are the single biggest pain points customers raise?
   - What exact words/phrases do they use?
   - What questions appear most on support tickets or sales calls?
   - What misconceptions do you correct repeatedly?

9. **Translate to keyword-style topics:** After the interview, convert each recurring
   question or pain point into a search phrase the way a customer would type it.
   Cross-check against autocomplete/PAA/related-searches lists to confirm real
   search phrasing.

### Consolidate and cluster

10. **Merge all three tracks** into one spreadsheet with columns:
    - Keyword/topic phrase
    - Inferred intent (informational, commercial, transactional)
    - Funnel stage (awareness, consideration, decision)
    - Source(s) of the signal (competitor, PAA, autocomplete, forum, SME)

11. **Cluster by shared intent:** Group terms that would naturally be answered by the
    same page or series of related pages. A coherent cluster has:
    - Shared semantic meaning and search intent
    - 6–12 supporting keywords per pillar
    - Coverage across funnel stages (awareness, consideration, decision)

Proceed to Step 5 with the fallback cluster table.

## Step 5: Internal quality check

Before showing output, review the generated clusters against these gates:

- **Completeness:** Each cluster has a pillar topic, 6–12 supporting keywords, and a
  clear rationale.
- **Coherence:** Keywords within each cluster share intent and would be answered by
  related pages, not disparate topics.
- **Strategic fit:** Clusters align with the business's actual offer and capabilities.
- **Funnel coverage:** Clusters span awareness, consideration, and decision stages
  (where applicable to the business model).

Fix any gaps before proceeding. If a cluster is incoherent or off-strategy, remove it
or split it.

## Step 6: Delimited output

Present all topic clusters in a single delimited block using this table format:

```
─────────────────────────────────────────────────────────────────
## Topic Clusters for SEO & Content Planning
─────────────────────────────────────────────────────────────────

| Pillar Topic | Seed Keywords | Estimated Demand Signal | Rationale |
| --- | --- | --- | --- |
| [Pillar keyword] | [comma-separated cluster keywords] | [Volume: X/mo, Difficulty: Y; or "Recurring PAA questions + competitor coverage" if fallback] | [Strategic fit: market opportunity, business relevance] |
| ... | ... | ... | ... |

─────────────────────────────────────────────────────────────────
```

Include:

- **Pillar Topic:** The broad, central keyword for each cluster
- **Seed Keywords:** 6–12 related, supporting long-tail variations
- **Estimated Demand Signal:** If tool-assisted, state search volume and difficulty
  (e.g., "850 searches/mo, KD 35"); if fallback, note the proxy signals (e.g., "Recurring
  PAA questions + 3+ competitors covering this + SME confirmation")
- **Rationale:** Why this cluster is worth investing in (market opportunity, strategic
  fit to business, proof of demand)

## Step 7: Register output and log learnings

Write the clusters document to `context/seo-research.md` by convention. **Apply
collision-check logic:** if the file already exists, append a `-N` suffix before `.md`
(try `-2`, then `-3`, etc.) until a unique filename is found. Never overwrite an
existing file.

Confirm the file was created, then add a row to the `## Context files` table in
`CLAUDE.md`. Use this format:

```markdown
| SEO research | `context/seo-research.md` | SEO research: keyword validation, topic clusters, search volume analysis, competitive keyword gaps, funnel-stage coverage |
```

The Summary must explicitly name "keyword", "SEO", "topic cluster", and "search volume"
— this wording is what makes the file legible to `cc-concept-content-strategy`'s Step 1
context-loading without that skill needing an edit. It is functionally part of this
requirement, not cosmetic.

Do **not** hand-edit the **Key Config Files** table — the pre-commit hook owns that sync.

Store learnings tagged `[cc-concept:cc-concept-seo-research]` in `.claude/learnings.md`.
Examples:

```
[cc-concept:cc-concept-seo-research] client markets B2B SaaS; avoid consumer-marketing keywords, prioritize "how to" and "vs" informational intents — 2026-07-20
[cc-concept:cc-concept-seo-research] Ubersuggest MCP tools available in session; keyword difficulty threshold appropriate for a mature domain (KD up to 60) — 2026-07-20
[cc-concept:cc-concept-seo-research] interview revealed customers use "platform" more than "tool"; adjust keyword focus accordingly — 2026-07-20
```

If the session revealed a preferred seed topic, a keyword or clustering pattern, or a
degrade-path detail, record it now.
