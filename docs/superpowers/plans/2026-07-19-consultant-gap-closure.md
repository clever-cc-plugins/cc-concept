# cc-concept Consultant-Grade Gap Closure Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Close five gaps identified by mapping the current `cc-concept`/`cc-content` skill set against the full agency value chain (Insight & Research, Strategy, Planning, Creation, Distribution, Measurement, Governance): no audience/persona development, no standalone competitive-research skill, no SEO/keyword research, no upfront measurement framework, and no engagement-level orchestration.

**Architecture:** Four new skill files under `plugins/cc-concept/skills/`, one two-file edit (`cc-concept-campaign-concept`, `cc-concept-gtm`) to add a Success Metrics section, and one small edit to `cc-concept-positioning` to delegate its existing inline competitive scan to the new standalone skill. No new `_shared/` framework files are required — each new skill reads/writes the existing `## Context files` table using the conventions already established in `_shared/skill-contract.md`. No compiled code, no unit-test runner — "tests" are structural (frontmatter parses as valid YAML, skill references resolve to real files) plus manual fixture runs.

**Tech Stack:** Markdown (skill files), `prettier` (repo's PostToolUse formatter), `python3` (frontmatter/YAML validity checks), `gitleaks` (pre-commit secret scan).

## Global Constraints

- **Source of truth for the gap list:** the value-chain gap analysis this plan implements (Insight & Research thin, Measurement half-built, no orchestration) — reproduced in the Task sections below rather than a separate spec doc, since each task's design decisions are self-contained.
- **Repo layout standard:** `marketplace/docs/cc-plugin-repo-guideline.md` — do not deviate.
- **Skills invoked by bare name**, never namespaced (`/cc-concept-audience`, not `/cc-concept:cc-concept-audience`).
- **No secrets** committed. **No `--force`** flags. Fix root causes, not symptoms.
- **Do not copy skill/plugin files between repos** — `cc-concept` and `cc-content` are independent git repos; cross-plugin references are by skill _name_ only (e.g., "hand off to `/cc-content-text`"), never by file path.
- **Every new skill adapts `_shared/skill-contract.md`'s 8-step sequence** unless a task explicitly documents why a step differs (matching the precedent set by `cc-concept-performance-review`).
- **Research-then-draft order is mandatory for every new skill in this plan.** Do not draft a SKILL.md from general knowledge alone — run the matching deep-research prompt (see companion research-prompt set) first, save the output under `docs/research/<skill-name>.md`, and cite specific findings in the skill's design-decisions comments or step content. This keeps the frameworks each skill selects from (persona templates, competitive-audit structures, SEO workflows) evidence-grounded rather than invented.
- **`CLAUDE.md`'s Key Config Files table is never hand-edited** — the pre-commit `sync-config-table.sh` hook owns it. Pre-populate descriptions before committing so the hook doesn't write a `TODO` row.
- **Learnings tags:** every new skill uses `[cc-concept:<skill-name>]` — never write to another plugin's tag.
- **`allowed-tools` expansions require justification inline** in the SKILL.md, same convention `cc-concept-positioning` already set when it gained `WebSearch, WebFetch`.

---

## File Structure

| Path                                                                 | Responsibility                                                                                                                                                                |
| -------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `docs/research/cc-concept-audience.md`                               | Saved deep-research output feeding Task 1                                                                                                                                     |
| `docs/research/cc-concept-competitive-research.md`                   | Saved deep-research output feeding Task 2                                                                                                                                     |
| `docs/research/cc-concept-seo-research.md`                           | Saved deep-research output feeding Task 3                                                                                                                                     |
| `docs/research/measurement-framework.md`                             | Saved deep-research output feeding Task 4                                                                                                                                     |
| `docs/research/cc-concept-orchestrator.md`                           | Saved deep-research output feeding Task 5                                                                                                                                     |
| `plugins/cc-concept/skills/cc-concept-audience/SKILL.md`             | New skill: interview-driven persona/ICP development, writes `context/audience-personas.md`                                                                                    |
| `plugins/cc-concept/skills/cc-concept-competitive-research/SKILL.md` | New skill: standalone competitive/market audit, writes `context/competitive-landscape.md`                                                                                     |
| `plugins/cc-concept/skills/cc-concept-positioning/SKILL.md`          | Edited: Step 1.5 competitive scan now delegates to `cc-concept-competitive-research` instead of an inline WebSearch/WebFetch call                                             |
| `plugins/cc-concept/skills/cc-concept-seo-research/SKILL.md`         | New skill: keyword/topic-cluster research, writes `context/seo-research.md`; uses Ubersuggest MCP tools when present, degrades to interview-based topic gathering when absent |
| `plugins/cc-concept/skills/cc-concept-campaign-concept/SKILL.md`     | Edited: adds a Success Metrics section (leading/lagging KPI tree, attribution approach, review cadence) to the generated campaign concept                                     |
| `plugins/cc-concept/skills/cc-concept-gtm/SKILL.md`                  | Edited: same Success Metrics section added to the generated GTM plan                                                                                                          |
| `plugins/cc-concept/skills/cc-concept-orchestrator/SKILL.md`         | New skill: given a stated business goal, sequences the right subset of existing + new `cc-concept`/`cc-content` skills and tracks progress through the arc                    |
| `CLAUDE.md`                                                          | +4 rows (three new skills, one net-new orchestrator) in Key Config Files table; pre-populated before commit                                                                   |
| `README.md`                                                          | +4 rows in the skill table                                                                                                                                                    |

Already present, unmodified: `_shared/skill-contract.md`, `_shared/campaign-frameworks.md`, `_shared/positioning-frameworks.md`, all other existing skill files.

---

## Task 1: `cc-concept-audience` — persona/ICP development

Deliverable: a new skill that runs a JTBD-style interview (or synthesizes from pasted customer data) to produce one or more audience personas, gated by nothing (same "discoverer" pattern as `cc-concept-onboarding`), and registers the result as context every other gated skill already knows how to consume.

**Files:**

- Research: `docs/research/cc-concept-audience.md` (produced by running Research Prompt 1 in a deep-research tool and saving the output here)
- Create: `plugins/cc-concept/skills/cc-concept-audience/SKILL.md`
- Reference (read, do not modify): `plugins/cc-concept/skills/cc-concept-onboarding/SKILL.md` (the interview/collision-check/registration pattern this skill reuses)
- Reference (read, do not modify): `plugins/cc-concept/skills/_shared/skill-contract.md`

**Interfaces:**

- Consumes: pasted customer data or interview answers; optionally reads `context/organization-background.md` if already registered (semantic match, not filename).
- Produces: `context/audience-personas.md` (collision-checked, e.g. `-2.md` suffix if a file already exists), plus a `## Context files` row with a Summary containing "audience", "persona", "ICP", "segment" keywords — this is what every other skill's existing "Target audience" gate already semantically matches against, so no downstream skill needs to change.

- [ ] **Step 1: Read the research output and select a persona framework**

Open `docs/research/cc-concept-audience.md`. Confirm it covers: JTBD interview question sets, B2B vs. B2C persona template differences, and how many personas is "enough" before diminishing returns. If any of the three is missing, re-run Research Prompt 1 with a narrower follow-up before continuing — do not fill the gap from general knowledge.

- [ ] **Step 2: Write the SKILL.md frontmatter**

```markdown
---
name: cc-concept-audience
description: >
  Use this skill to develop one or more audience personas or ICPs from scratch —
  interviewing the owner or synthesizing from pasted customer data (support tickets,
  sales call notes, survey results). Invoke when the user asks to "build a persona",
  "define our ICP", "who is our target audience", "develop buyer personas", or when
  another cc-concept skill reports that its "target audience" need is missing.
  Produces `context/audience-personas.md` for every other skill's existing audience
  gate to consume — this skill is the producer other skills already assumed existed.
allowed-tools: Read, Write, Edit, Bash
argument-hint: "[optional: path to customer data to synthesize personas from]"
---
```

- [ ] **Step 3: Write Steps 0–2 of the skill body**

```markdown
# Audience Persona Development Skill

Every other `cc-concept` and `cc-content` skill gates on "target audience" as
something already known. This skill is where it gets built, so gated skills upstream
of it stop asking the owner to describe an audience from memory.

Adapts `../_shared/skill-contract.md`'s 8-step sequence. Step 1 differs: this skill
has no required gate of its own (it is a discoverer, like `cc-concept-onboarding`),
but it still loads organization background if registered, since persona work grounded
in a known mission/offer beats personas built in isolation.

## Step 0: Recall learnings

If `.claude/learnings.md` exists, read it silently, all plugin tags. Apply relevant
entries (e.g., a prior run's preferred persona count or template). Never announce.

## Step 1: Load context and choose a mode

Read the `## Context files` table. If `context/organization-background.md` (or
equivalent Summary match) exists, load it — persona work references the org's actual
offer and constraints rather than generic language.

Ask once: "Do you have existing customer data (support tickets, sales notes, survey
results, interview transcripts) to synthesize personas from, or should I interview
you to build one from scratch?" Branch on the answer:

- **Synthesize mode:** read the supplied file(s)/pasted text; extract patterns across
  the [N: from research — number of raw inputs the research found sufficient for a
  defensible persona] cases before drafting.
- **Interview mode:** run the JTBD question set from `docs/research/cc-concept-audience.md`
  §[N: exact section], one question at a time, same one-at-a-time interview rhythm as
  `cc-concept-onboarding`.
```

- [ ] **Step 4: Write Steps 3–7, informed directly by the research file's persona template**

Using the exact template `docs/research/cc-concept-audience.md` recommends (jobs/pains/gains, or an alternative structure the research surfaced), write:

- Step 3 (Calibrate): how many personas to produce this run — default to the research's recommended ceiling before diminishing returns, ask the owner to confirm.
- Step 4 (Generate): the persona document structure itself, one persona block per identified segment.
- Step 5 (Internal quality check): a checklist gate — each persona must be falsifiable (specific enough that later performance-review could contradict it), not a demographic sketch.
- Step 6 (Delimited output): present all personas in one delimited block before writing anything.
- Step 7 (Feedback + registration): collision-checked write to `context/audience-personas.md`; `## Context files` row with the keyword-rich Summary from the Interfaces section above; learnings tagged `[cc-concept:cc-concept-audience]`.

- [ ] **Step 5: Manual fixture test**

Run the skill twice against a throwaway test project: once in interview mode (answer the JTBD questions for a fictional B2B SaaS), once in synthesize mode (paste three fabricated support-ticket excerpts). Confirm both produce a `context/audience-personas.md` and a correctly-appended `## Context files` row. Confirm running `/cc-concept-positioning` afterward silently picks up the new file without being told about it (Step 1's semantic match should just work).

- [ ] **Step 6: Update CLAUDE.md and README.md rows, then commit**

Pre-populate the `CLAUDE.md` Key Config Files row and the `README.md` skill-table row (do not leave them for the pre-commit hook to fill with a TODO).

```bash
git add plugins/cc-concept/skills/cc-concept-audience/SKILL.md CLAUDE.md README.md docs/research/cc-concept-audience.md
git commit -m "feat: add cc-concept-audience persona/ICP development skill"
```

---

## Task 2: `cc-concept-competitive-research` — standalone competitive/market audit

Deliverable: promote the competitive scan currently buried as an optional Step 1.5 inside `cc-concept-positioning` into its own first-class skill, so a competitive audit can be run independent of a positioning exercise and reused by `cc-concept-gtm`, `cc-concept-channel-advisor`, and `cc-concept-content-strategy`.

**Files:**

- Research: `docs/research/cc-concept-competitive-research.md` (Research Prompt 2)
- Create: `plugins/cc-concept/skills/cc-concept-competitive-research/SKILL.md`
- Modify: `plugins/cc-concept/skills/cc-concept-positioning/SKILL.md` — replace the inline competitive-scan step with a one-line delegation

**Interfaces:**

- Consumes: `context/organization-background.md` if present; `WebSearch`/`WebFetch` for public competitor content.
- Produces: `context/competitive-landscape.md` (collision-checked) — the exact Summary keyword set (`competitor`, `competitive landscape`, `market gap`) that `cc-concept-onboarding`'s coverage check and `cc-concept-positioning`'s existing gate already look for, so no other skill's gating logic changes.

- [ ] **Step 1: Read the research output and confirm audit structure**

Confirm `docs/research/cc-concept-competitive-research.md` covers: a repeatable competitive-teardown structure (messaging audit, SWOT, share-of-voice, content-gap analysis) and how many competitors is enough for a defensible read (the research the team already has suggests 2–4; confirm or update from the new research).

- [ ] **Step 2: Write the SKILL.md frontmatter**

```markdown
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
```

- [ ] **Step 3: Write the skill body**, structured around the research file's teardown framework: Step 1 identifies 2–4 named or inferred competitors (ask once if none named and organization background gives no obvious candidates); Step 4 (Generate) runs the audit structure per competitor (messaging themes, stated/apparent differentiation, evident gaps); Step 6 output is a delimited per-competitor breakdown plus a synthesized "underserved angles" summary; Step 7 registers `context/competitive-landscape.md`.

- [ ] **Step 4: Edit `cc-concept-positioning` to delegate**

Replace the existing inline "optional competitive content scan" step with: "If competitive landscape is not yet loaded, offer to run `/cc-concept-competitive-research` before continuing; proceed with whatever context is already registered if declined." Remove the now-redundant `WebSearch, WebFetch` entries from `cc-concept-positioning`'s `allowed-tools` frontmatter (the capability moves to the new skill) — confirm no other step in that file still calls them before removing.

- [ ] **Step 5: Manual fixture test**

Run `/cc-concept-competitive-research` standalone naming three fictional competitors; confirm `context/competitive-landscape.md` is written. Run `/cc-concept-positioning` afterward and confirm it detects the file via semantic match and skips its own delegation offer.

- [ ] **Step 6: Update CLAUDE.md/README.md rows (new skill + edited positioning row), then commit**

```bash
git add plugins/cc-concept/skills/cc-concept-competitive-research/SKILL.md plugins/cc-concept/skills/cc-concept-positioning/SKILL.md CLAUDE.md README.md docs/research/cc-concept-competitive-research.md
git commit -m "feat: promote competitive scan to standalone cc-concept-competitive-research skill"
```

---

## Task 3: `cc-concept-seo-research` — keyword/topic-cluster research

Deliverable: a new skill that produces keyword-validated topic clusters, using the Ubersuggest MCP tools when the user's environment has them connected, and degrading gracefully to interview-based topic gathering when it doesn't — feeding `cc-concept-content-strategy`'s pillar/cluster generation with actual search-demand data instead of guesses.

**Files:**

- Research: `docs/research/cc-concept-seo-research.md` (Research Prompt 3)
- Create: `plugins/cc-concept/skills/cc-concept-seo-research/SKILL.md`
- Reference (read, do not modify): `plugins/cc-concept/skills/cc-concept-content-strategy/SKILL.md` (the exact Summary keywords its Step 1 load already looks for, so the new skill's output registers under a Summary that skill will find without being edited)

**Interfaces:**

- Consumes: `context/organization-background.md`, `context/audience-personas.md` if present (from Task 1); Ubersuggest MCP tools (`keyword_suggestions`, `content_ideas`, `serp_analysis`, `domain_overview`) _if available in the current session_ — detect by attempting one low-cost call and catching absence, never by assuming the MCP is installed.
- Produces: `context/seo-research.md` (collision-checked) with a Summary containing "keyword", "SEO", "topic cluster", "search volume" — read by `cc-concept-content-strategy`'s existing Step 1 without that skill needing an edit.

- [ ] **Step 1: Read the research output and confirm the degrade path**

Confirm `docs/research/cc-concept-seo-research.md` documents both a tool-assisted workflow (keyword volume/difficulty, SERP gap analysis, content-idea generation) and a no-tool fallback workflow (competitor-content keyword inference, question-based topic gathering via interview). A skill that hard-fails without a specific MCP violates this plugin family's degrade-gracefully convention (same one `cc-content-blog-article` uses for missing brand voice) — do not skip the fallback path.

- [ ] **Step 2: Write the SKILL.md frontmatter**

```markdown
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
```

- [ ] **Step 3: Write the skill body**, Step 1 detecting MCP availability (try `mcp__claude_ai_Ubersuggest__keyword_suggestions` with a trivial seed; on error or absence, state once "SEO tooling isn't connected this session — continuing with interview-based topic gathering" and proceed, never treating this as a blocking gate); Step 4 (Generate) branching into the tool-assisted or fallback workflow per the research file; Step 6 delimited output as a topic-cluster table (cluster name, seed keywords, estimated demand signal if tool-assisted, rationale if fallback); Step 7 registers `context/seo-research.md`.

- [ ] **Step 4: Manual fixture test**

Run once assuming no MCP connected (simulate by not loading the Ubersuggest tools) — confirm the skill states the degrade notice once and still produces a usable topic-cluster table via interview. If Ubersuggest MCP tools are available in this environment, run a second fixture test with a real seed keyword and confirm actual `keyword_suggestions` data appears in the output.

- [ ] **Step 5: Update CLAUDE.md/README.md, then commit**

```bash
git add plugins/cc-concept/skills/cc-concept-seo-research/SKILL.md CLAUDE.md README.md docs/research/cc-concept-seo-research.md
git commit -m "feat: add cc-concept-seo-research keyword and topic-cluster skill"
```

---

## Task 4: Upfront measurement framework — extend `cc-concept-campaign-concept` and `cc-concept-gtm`

Deliverable: both skills gain a Success Metrics section in their generated output, defined _before_ the campaign/launch runs — closing the gap where both performance-review skills only ever look backward.

**Files:**

- Research: `docs/research/measurement-framework.md` (Research Prompt 4)
- Modify: `plugins/cc-concept/skills/cc-concept-campaign-concept/SKILL.md`
- Modify: `plugins/cc-concept/skills/cc-concept-gtm/SKILL.md`
- Reference (read, do not modify): `plugins/cc-concept/skills/cc-concept-performance-review/SKILL.md` (Step 2's bet-extraction format — the new Success Metrics section must emit bets in the _same_ `Bet: [claim] | Expected signal: [result] | Source: [document+section]` shape that skill already parses, so no edit is needed there)

**Interfaces:**

- Consumes: whatever business goals/KPIs context is already gated in both skills — no new context need introduced.
- Produces: an additional "Success Metrics" block in each skill's existing delimited output, containing 2–4 leading/lagging KPI pairs, a stated attribution approach, and a review cadence — written in the exact bet shape `cc-concept-performance-review` already extracts, so that skill's Step 2 recognizes it as source material with zero changes on its side.

- [ ] **Step 1: Read the research output and select a KPI-tree structure**

Confirm `docs/research/measurement-framework.md` covers: leading-vs-lagging metric pairing per campaign/launch type, common attribution-model tradeoffs (last-touch, multi-touch, self-reported), and typical review-cadence conventions (weekly during launch, monthly steady-state).

- [ ] **Step 2: Add the Success Metrics step to `cc-concept-campaign-concept`**

Insert a new step immediately after the existing "Creative brief" generation step (do not renumber steps that already exist elsewhere in the file — insert as e.g. Step 5a). Content: for the campaign's stated business goals, produce 2–4 KPI pairs (one leading, one lagging) using the research file's pairing table for the resolved campaign type (product-launch, thought-leadership, seasonal-promotion, retention, lead-generation, brand-awareness); state the attribution approach in one sentence; state a review cadence. Emit each pair in the bet shape: `Bet: [claim] | Expected signal: [result] | Source: campaign concept §Success Metrics`.

- [ ] **Step 3: Add the equivalent Success Metrics step to `cc-concept-gtm`**

Same content shape, inserted after the existing "Launch milestones" step, with bets keyed to milestones rather than campaign goals: `Bet: [milestone] | Expected signal: [result] | Source: GTM plan §Success Metrics`.

- [ ] **Step 4: Update each skill's Quality gates list**

Add "Success Metrics present and in bet-shape" as a new gate in both skills' existing Quality gates section (Completeness, extractability, framework alignment, consistency) — do not remove or reorder the existing gates.

- [ ] **Step 5: Manual fixture test**

Run `/cc-concept-campaign-concept` and `/cc-concept-gtm` against the same fictional test project used in Task 1/2's fixtures. Confirm both outputs now include a Success Metrics block in the exact bet shape. Then run `/cc-concept-performance-review` against both and confirm Step 2 extracts the new bets without any special-casing — if it doesn't recognize them, the bet-shape string in Steps 2–3 above needs to match `cc-concept-performance-review`'s parser exactly; fix the shape, not the parser.

- [ ] **Step 6: Update CLAUDE.md rows for both edited skills, then commit**

```bash
git add plugins/cc-concept/skills/cc-concept-campaign-concept/SKILL.md plugins/cc-concept/skills/cc-concept-gtm/SKILL.md CLAUDE.md docs/research/measurement-framework.md
git commit -m "feat: add upfront success-metrics framework to campaign-concept and gtm"
```

---

## Task 5: `cc-concept-orchestrator` — engagement-level sequencing

Deliverable: a new skill that, given a stated business goal ("launch a product," "grow our LinkedIn presence," "reposition against a new competitor"), recommends and sequences the specific subset and order of existing `cc-concept`/`cc-content` skills needed — turning the 21-skill toolbox into a guided arc. This task depends on Tasks 1–4 being merged first, since the orchestrator's sequencing logic names them.

**Files:**

- Research: `docs/research/cc-concept-orchestrator.md` (Research Prompt 5)
- Create: `plugins/cc-concept/skills/cc-concept-orchestrator/SKILL.md`
- Reference (read, do not modify): every other `plugins/cc-concept/skills/*/SKILL.md` and `plugins/cc-content/skills/*/SKILL.md` frontmatter `description` field (this skill's sequencing logic must name real, current skills — re-read the frontmatter at authoring time, don't rely on the list in this plan going stale)

**Interfaces:**

- Consumes: a free-text business goal from the user; the current `## Context files` table (to know what's already in place and skip redundant steps).
- Produces: no new context file — output is a numbered execution plan (which skill, in what order, why, and what it depends on already being registered), presented in a delimited block; the user runs each named skill themselves, one at a time. This skill never invokes other skills directly — it recommends, matching this plugin family's existing convention of offering deferral (`cc-concept-marketing-advisor`) rather than auto-chaining.

- [ ] **Step 1: Read the research output and define the goal taxonomy**

Confirm `docs/research/cc-concept-orchestrator.md` covers common top-level marketing engagement types (product launch, brand repositioning, always-on content growth, campaign-specific push) and, for each, which stages of the value chain (Insight → Strategy → Planning → Creation → Distribution → Measurement) are actually needed — not every engagement needs every stage.

- [ ] **Step 2: Write the SKILL.md frontmatter**

```markdown
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
```

- [ ] **Step 3: Write the skill body**

Step 1: classify the stated goal against the research file's taxonomy (ask once to disambiguate if it matches more than one type equally well). Step 2: read the `## Context files` table; mark which of {organization background, audience personas, competitive landscape, positioning, content strategy, SEO research} are already registered. Step 4 (Generate): produce a numbered sequence — for each still-missing prerequisite, name the specific skill that produces it (`cc-concept-audience`, `cc-concept-competitive-research`, `cc-concept-seo-research`, `cc-concept-positioning`); for the goal-specific planning/creation stages, name the specific downstream skills (`cc-concept-campaign-concept` or `cc-concept-gtm`, then `cc-concept-content-strategy`, then the relevant `cc-content-*` drafting skills, then `cc-content-atomize` if multiple formats are named, then the relevant performance-review skill). Step 6: delimited output as a numbered list with one-line rationale per step and an explicit "already in place, skip" marker for prerequisites already registered.

- [ ] **Step 4: Manual fixture test**

Run against three different stated goals ("launch a new product," "we've never done any strategy work and want to start posting on LinkedIn," "a competitor just repositioned, help us respond") against the fixture project from earlier tasks (which by now has personas, competitive landscape, and campaign-concept registered from Tasks 1–4's fixtures). Confirm the sequencing correctly marks already-registered prerequisites as "skip" rather than re-recommending `cc-concept-audience` etc.

- [ ] **Step 5: Update CLAUDE.md/README.md, then commit**

```bash
git add plugins/cc-concept/skills/cc-concept-orchestrator/SKILL.md CLAUDE.md README.md docs/research/cc-concept-orchestrator.md
git commit -m "feat: add cc-concept-orchestrator engagement-sequencing skill"
```

---

## Self-Review

- **Coverage:** Task 1 → audience/persona gap. Task 2 → standalone competitive-research gap. Task 3 → SEO/keyword gap. Task 4 → upfront measurement gap. Task 5 → orchestration gap. All five gaps from the analysis have a task.
- **Placeholder scan:** every step names an exact file, an exact frontmatter block, or an exact test action; bracketed `[N: ...]` markers appear only where the value is genuinely determined by the research output the task requires reading first, not as a stand-in for undone thinking.
- **Type/shape consistency:** the Success Metrics bet shape in Task 4 is defined once and reused verbatim (`Bet: [claim] | Expected signal: [result] | Source: [...]`) — matches `cc-concept-performance-review`'s existing Step 2 parser, confirmed by cross-reference rather than assumption.
- **Ordering:** Task 5 explicitly depends on Tasks 1–4; the other four are independent and can run in parallel via `superpowers:subagent-driven-development`.
