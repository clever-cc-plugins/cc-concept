# cc-concept Slice 4 (Planning Skills) Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add the `cc-concept-content-strategy` and `cc-concept-gtm` skills to the existing `cc-concept` plugin — an editorial planning skill built on Message House pillars, and a go-to-market launch planning skill built on the SOSTAC+RACE+Message House composite already used by campaign-concept.

**Architecture:** Two new Markdown files under the existing `cc-concept` plugin repo (`plugins/cc-concept/skills/`), following the same shape as Slices 1–3's skills. No new `_shared/` file — both reuse `_shared/campaign-frameworks.md` directly. No new infra, no new plugin registration. There is no compiled code and no unit-test runner; "tests" are structural assertions (`grep`, `python3` YAML parse) plus a final round of manual fixture runs (spec §5).

**Tech Stack:** Markdown (skill files), `prettier` (repo's PostToolUse formatter), `python3` (frontmatter/YAML validity checks), `gitleaks` (pre-commit secret scan).

## Global Constraints

- **Design source of truth:** `docs/superpowers/specs/2026-07-19-cc-concept-slice4-planning-skills-design.md`. Every task traces to it.
- **Repo layout standard:** `marketplace/docs/cc-plugin-repo-guideline.md` — do not deviate.
- **Plugin name:** `cc-concept` (already scaffolded). Skills invoked by bare name (`/cc-concept-content-strategy`, `/cc-concept-gtm`), never namespaced.
- **No secrets** committed. **No `--force`** flags. Fix root causes.
- **Do not copy skill/plugin files between repos.**
- **Learnings tag formats:** `[cc-concept:cc-concept-content-strategy] <observation> — <YYYY-MM-DD>` and `[cc-concept:cc-concept-gtm] <observation> — <YYYY-MM-DD>`.
- **Context model:** free-form `## Context files` table (`| Label | File | Summary |`); skills match on the **Summary** column semantically, never on label or filename.
- **Gated needs for both skills** (this slice's OQ-007 resolution): exactly two — **business goals** and **target audience** — three-state model (covered / absent-but-supplied-ask-once / absent-and-unanswered-degraded), evaluated independently, same pattern as `cc-concept-campaign-concept` and `cc-concept-channel-advisor`.
- **Content strategy framework:** Message House only, from `plugins/cc-concept/skills/_shared/campaign-frameworks.md` — no new framework file. Content pillars ≡ Message House pillars.
- **GTM framework:** SOSTAC + RACE + Message House, all from the same file — the same composable-by-facet model campaign-concept applies.
- **Launch types (FR-071):** `product-launch`, `feature-release`, `market-expansion`.
- **Degraded-output prefix:** matches the mechanic already shipped in `cc-concept-campaign-concept` / `cc-concept-channel-advisor` — `⚠ DEGRADED OUTPUT — generated without: <needs>` prefixed before the delimiter block when Step 2 lands in the degraded state for either or both gated needs; omitted otherwise.
- **Content strategy registration (FR-062):** collision-checked new context file (same numbering scheme as positioning), with a Summary explicitly naming "content strategy," "pillars," and "topic clusters" so `cc-content-blog-article`/`cc-content-linkedin-post` pick it up by semantic match.
- **GTM brief.md by-product (FR-072):** reuses campaign-concept's exact collision-check mechanic (overwrite / save-as / cancel) verbatim; not registered in the `## Context files` table, same rule as campaign-concept's brief.md.

---

## File Structure

| Path                                                             | Responsibility                                                       |
| ---------------------------------------------------------------- | -------------------------------------------------------------------- |
| `plugins/cc-concept/skills/cc-concept-content-strategy/SKILL.md` | Editorial planning: content pillars, topic clusters, mix, cadence    |
| `plugins/cc-concept/skills/cc-concept-gtm/SKILL.md`              | Go-to-market launch planning, optional brief.md by-product           |
| `CLAUDE.md`                                                      | +2 rows in the Key Config Files table for the two new SKILL.md files |

Already present: `docs/superpowers/specs/2026-07-19-cc-concept-slice4-planning-skills-design.md`, this plan file, `_shared/skill-contract.md`, `_shared/campaign-frameworks.md`, `_shared/positioning-frameworks.md` (all prior slices, unmodified), `cc-concept-onboarding/SKILL.md`, `cc-concept-positioning/SKILL.md`, `cc-concept-campaign-concept/SKILL.md`, `cc-concept-marketing-advisor/SKILL.md`, `cc-concept-channel-advisor/SKILL.md` (all prior slices, unmodified).

---

## Task 1: Content strategy skill

Deliverable: `cc-concept-content-strategy/SKILL.md` — an editorial planning skill built on Message House pillars, gated on business goals + target audience, that registers its output as project context (spec §2).

**Files:**

- Create: `plugins/cc-concept/skills/cc-concept-content-strategy/SKILL.md`
- Depends on: `_shared/skill-contract.md`, `_shared/campaign-frameworks.md` (Message House section)
- Reference (read for shape, do not modify): `plugins/cc-concept/skills/cc-concept-positioning/SKILL.md` (for the collision-check/registration pattern used in Step 6.5)

**Interfaces:**

- Consumes: the `## Context files` table (business goals + target audience Summaries, preferring a `cc-concept-positioning` output file); `../_shared/campaign-frameworks.md`'s Message House section; the shared contract.
- Produces: a collision-checked context file (registered in the `## Context files` table) that `cc-content-blog-article`/`cc-content-linkedin-post` can pick up by Summary match.

- [ ] **Step 1: Write the SKILL.md frontmatter**

```markdown
---
name: cc-concept-content-strategy
description: >
  Use this skill to produce an editorial planning framework covering content pillars,
  topic clusters, content type mix, and publishing cadence. Invoke when the user asks
  for a "content strategy", "editorial plan", "content pillars", or "topic clusters".
  Produces a content strategy document and registers it as project context so
  cc-content skills can align individual pieces to it.
allowed-tools: Read, Write, Edit, Bash
argument-hint: "[optional: brief or focus for the content strategy]"
---
```

- [ ] **Step 2: Write the skill body**

Body must contain, in order:

1. Intro (H1 `# Content Strategy Skill`, then a short paragraph): this skill produces an editorial planning framework — content pillars, topic clusters, content mix, and cadence — and registers the output as project context so `cc-content` skills automatically align individual pieces to it.
2. **Contract reference:** `This skill follows the shared step sequence in ../_shared/skill-contract.md. Steps below add only content-strategy-specific behavior.`
3. **Step 0–1** (`## Step 0–1: Recall learnings and load context`): recall learnings silently. Load the `## Context files` table by Summary. State explicitly: look for **business goals/KPIs** and **target audience** (the two gated needs, preferring a `cc-concept-positioning` output file if one is registered); note silently if present, never ask about: brand voice, existing content inventory, competitive landscape.
4. **Step 2** (`## Step 2: Gating — Three-State Model`): gate on **exactly two** needs — **business goals** and **target audience**. For each, resolve one of three states — **covered** (use silently, no ask), **absent-but-supplied** (ask once, user answers → use, non-degraded), **absent-and-unanswered** (asked once, no usable answer → that section labelled **⚠ DEGRADED**, never fabricated, rest still generates).

   **Check business goals.** Search the context table Summary column for semantic matches: business goals, KPIs, objectives, targets, growth stage, success metrics. If covered, use silently. If absent, ask once:

   > "I need to understand what this content strategy should support. Briefly: What are your primary business goals or KPIs right now? (e.g. revenue growth, lead volume, retention, brand awareness) Is there a specific target or metric this content strategy should move?"

   If the user provides a usable answer, proceed non-degraded. If they decline or the answer is too vague to use, label the section `## Business Goals ⚠ DEGRADED` in the output and continue.

   **Check target audience.** Search the context table Summary column for semantic matches: target audience, positioning, organization background, customer segments, buyer profile. Prefer a `cc-concept-positioning` output file's Summary if one is registered; else fall back to organization background. If covered, use silently. If absent, ask once:

   > "I need to understand who this content is for. Briefly: Who is the target audience? (role, company type/size if B2B, or demographic if B2C) What stage are they typically at when they encounter your content? (just learning you exist, actively comparing options, or already a customer)"

   If the user provides a usable answer, proceed non-degraded. If they decline or the answer is too vague to use, label the section `## Target Audience ⚠ DEGRADED` in the output and continue.

5. **Step 3** (`## Step 3: Calibrate`): `Infer funnel stage and audience type from loaded context. Present a one-line inference summary and wait for user confirmation or correction before drafting.` Include this exact example: `"Audience: B2B mid-market · Goal: lead generation · Funnel focus: MOFU"`.
6. **Step 4** (`## Step 4: Generate`): apply Message House from `../_shared/campaign-frameworks.md`. **State the choice before generating.** Example:

   > "Using Message House for content pillar architecture."

   Produce a content strategy that includes:

   - **Content pillars** — at least two, each a Message House pillar, each with supporting topic clusters.
   - **Content type mix** — a recommended mix of content types (e.g. blog, video, social, case study) with rationale tied to the inferred funnel stage (TOFU skews video/social; BOFU skews case studies/comparisons).
   - **Publishing cadence** — a suggested frequency per content type.

7. **Step 5–6** (`## Step 5–6: Quality check and delimited output`) per contract: the quality check must explicitly verify all three elements above are present (at least two pillars, each with topic clusters). Then this exact instruction, matching the mechanic already shipped in `cc-concept-campaign-concept`:

   State: `If Step 2 ended in a degraded state for one or both gated needs (business goals and/or target audience), prefix the output with:` followed by a one-line code span `⚠ DEGRADED OUTPUT — generated without: <comma-separated list of unmet needs>`.

   Then state: `For example, if target audience is degraded but business goals are not, prefix with:` followed by the code span `⚠ DEGRADED OUTPUT — generated without: target audience`. `If both are degraded, prefix with:` followed by the code span `⚠ DEGRADED OUTPUT — generated without: business goals, target audience`. `If neither need is degraded, omit the prefix.`

   Then: `Return the content strategy inside clear delimiters:` followed by this fenced block (a single level of triple-backtick fencing, written literally into the SKILL.md body — do not nest it inside another fence):

   ```
   ─────────────────────────────────────────────────────────────────
   ## Content Strategy
   ─────────────────────────────────────────────────────────────────

   [Generated content strategy here]

   ─────────────────────────────────────────────────────────────────
   ```

8. **Step 6.5** (`## Step 6.5: Register output`): write the content strategy document to `context/content-strategy.md` by convention. **Apply collision-check logic**: if the file already exists, append a `-N` suffix before `.md` (try `-2`, then `-3`, etc.) until a filename that does not already exist is found — never overwrite an existing file. Confirm the file was created, then add a row to the `## Context files` table in `CLAUDE.md`. Include this exact example row:

   ```markdown
   | Content strategy | `context/content-strategy.md` | Editorial planning framework: content pillars, topic clusters, content type mix, publishing cadence |
   ```

   State explicitly: `The Summary must explicitly name "content strategy," "pillars," and "topic clusters" — this wording is what makes the file legible to cc-content-blog-article and cc-content-linkedin-post's Summary-matching; it is functionally part of this requirement, not cosmetic (FR-062).` Do **not** hand-edit the **Key Config Files** table — the pre-commit hook owns that sync.

9. **Step 7** (`## Step 7: Feedback`) per contract: store learnings tagged `[cc-concept:cc-concept-content-strategy]`. Include these two example entries verbatim:

   ```
   [cc-concept:cc-concept-content-strategy] client prefers thought-leadership pillars over product-led pillars, positions as an industry voice — 2026-07-19
   [cc-concept:cc-concept-content-strategy] client publishes weekly on LinkedIn but only monthly long-form; cadence recommendations should respect that split — 2026-07-19
   ```

- [ ] **Step 3: Verify frontmatter and the gating/framework/registration markers**

Run:

```bash
f=plugins/cc-concept/skills/cc-concept-content-strategy/SKILL.md
python3 - "$f" <<'PY'
import sys, yaml
meta = yaml.safe_load(open(sys.argv[1]).read().split('---')[1])
assert meta['name'] == 'cc-concept-content-strategy', meta.get('name')
assert 'allowed-tools' in meta
print("frontmatter OK")
PY
grep -q 'skill-contract.md' "$f" && echo "contract ref OK"
grep -q 'campaign-frameworks.md' "$f" && grep -q -i 'Message House' "$f" && echo "framework ref OK"
grep -q -i 'business goals' "$f" && grep -q -i 'target audience' "$f" && echo "two needs OK"
grep -q -i 'DEGRADED' "$f" && grep -q -i 'once' "$f" && echo "three-state OK"
grep -q -i 'DEGRADED OUTPUT — generated without' "$f" && echo "degraded-output prefix OK"
grep -q -i 'content pillars' "$f" && grep -q -i 'topic clusters' "$f" && echo "pillars/clusters OK"
grep -q -i 'collision-check' "$f" && grep -q -i 'context/content-strategy.md' "$f" && echo "registration OK"
grep -q -i 'not cosmetic' "$f" && echo "summary-legibility note OK"
```

Expected: `frontmatter OK`, `contract ref OK`, `framework ref OK`, `two needs OK`, `three-state OK`, `degraded-output prefix OK`, `pillars/clusters OK`, `registration OK`, `summary-legibility note OK`.

- [ ] **Step 4: Commit**

```bash
git add plugins/cc-concept/skills/cc-concept-content-strategy/SKILL.md
git commit -m ":sparkles: feat(cc-concept): add content strategy skill"
```

---

## Task 2: GTM skill

Deliverable: `cc-concept-gtm/SKILL.md` — a go-to-market launch planning skill built on the SOSTAC+RACE+Message House composite, gated on business goals + target audience, with an optional brief.md by-product (spec §3).

**Files:**

- Create: `plugins/cc-concept/skills/cc-concept-gtm/SKILL.md`
- Depends on: `_shared/skill-contract.md`, `_shared/campaign-frameworks.md` (all three frameworks), `_shared/positioning-frameworks.md` (fallback positioning generation)
- Reference (read for shape, do not modify): `plugins/cc-concept/skills/cc-concept-campaign-concept/SKILL.md` (this skill's Step 4 composite application and Step 6.5 collision-check must match its exact pattern)

**Interfaces:**

- Consumes: the `## Context files` table (business goals + target audience Summaries, preferring a `cc-concept-positioning` output file); `../_shared/campaign-frameworks.md`'s SOSTAC/RACE/Message House; `../_shared/positioning-frameworks.md` (fallback only); the shared contract.
- Produces: a delimited GTM plan; optionally `brief.md` in the working-directory root (collision-checked, **not** registered as context).

- [ ] **Step 1: Write the SKILL.md frontmatter**

```markdown
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
```

- [ ] **Step 2: Write the skill body**

Body must contain, in order:

1. Intro (H1 `# Go-to-Market Skill`, then a short paragraph): this skill structures a launch plan for a new product, service, feature, or market entry, and optionally hands off a `brief.md`-compatible campaign brief as a by-product.
2. **Contract reference:** `This skill follows the shared step sequence in ../_shared/skill-contract.md. Steps below add only GTM-specific behavior.`
3. **Step 0–1** (`## Step 0–1: Recall learnings and load context`): recall learnings silently. Load the `## Context files` table by Summary. State explicitly: look for **business goals/KPIs** and **target audience** (the two gated needs, preferring a `cc-concept-positioning` output file if one is registered); note silently if present, never ask about: competitive landscape, current marketing channels, existing positioning depth.
4. **Step 2** (`## Step 2: Gating — Three-State Model`): gate on **exactly two** needs — **business goals** and **target audience**. For each, resolve one of three states — **covered** (use silently, no ask), **absent-but-supplied** (ask once, user answers → use, non-degraded), **absent-and-unanswered** (asked once, no usable answer → that section labelled **⚠ DEGRADED**, never fabricated, rest still generates).

   **Check business goals.** Search the context table Summary column for semantic matches: business goals, KPIs, objectives, targets, growth stage, success metrics. If covered, use silently. If absent, ask once:

   > "I need to understand what this launch should achieve. Briefly: What are your primary business goals or KPIs for this launch? (e.g. revenue growth, lead volume, market share, brand awareness) Is there a specific target or metric this launch should move?"

   If the user provides a usable answer, proceed non-degraded. If they decline or the answer is too vague to use, label the section `## Business Goals ⚠ DEGRADED` in the output and continue.

   **Check target audience.** Search the context table Summary column for semantic matches: target audience, positioning, organization background, customer segments, buyer profile. Prefer a `cc-concept-positioning` output file's Summary if one is registered; else fall back to organization background. If covered, use silently. If absent, ask once:

   > "I need to understand who this launch is for. Briefly: Who is the target audience? (role, company type/size if B2B, or demographic if B2C) What stage are they typically at when they encounter this launch? (just learning you exist, actively comparing options, or already a customer)"

   If the user provides a usable answer, proceed non-degraded. If they decline or the answer is too vague to use, label the section `## Target Audience ⚠ DEGRADED` in the output and continue.

5. **Step 3** (`## Step 3: Calibrate`): `If --type was passed in $ARGUMENTS, use it directly and skip the launch-type question. Otherwise infer the launch type from loaded context; where inference isn't confident, ask directly rather than guessing. Present a one-line inference summary and wait for user confirmation or correction before drafting.` Include this exact scaling guidance:

   ```markdown
   - **product-launch** — full-depth treatment across all output elements.
   - **feature-release** — lighter treatment; assumes existing audience and positioning are already known, focuses on messaging and milestones.
   - **market-expansion** — emphasizes audience redefinition and channel sequencing for the new market.
   ```

6. **Step 4** (`## Step 4: Generate`): apply SOSTAC, RACE, and Message House from `../_shared/campaign-frameworks.md` per that file's facet mapping. **State the mapping being applied** before generating. Example:

   > "Structuring with SOSTAC; sequencing channels with RACE; messaging with Message House."

   Produce a GTM plan that includes:

   - **Target audience definition** — the specific segment(s) this launch addresses.
   - **Positioning statement for the launch** — derived from loaded positioning context if present; otherwise generated fresh by following the selection process in `../_shared/positioning-frameworks.md`.
   - **Channel sequence with timing** — proposed channels sequenced by RACE stage, with a rough timeline.
   - **Key messages** — Message House pillars grounded in loaded context.
   - **Launch milestones** — at least three, tied to the Control facet of SOSTAC.

7. **Step 5–6** (`## Step 5–6: Quality check and delimited output`) per contract: the quality check must explicitly verify all five elements above are present, including that at least three milestones are listed. Then this exact instruction, matching the mechanic already shipped in `cc-concept-campaign-concept`:

   State: `If Step 2 ended in a degraded state for one or both gated needs (business goals and/or target audience), prefix the output with:` followed by a one-line code span `⚠ DEGRADED OUTPUT — generated without: <comma-separated list of unmet needs>`.

   Then state: `For example, if target audience is degraded but business goals are not, prefix with:` followed by the code span `⚠ DEGRADED OUTPUT — generated without: target audience`. `If both are degraded, prefix with:` followed by the code span `⚠ DEGRADED OUTPUT — generated without: business goals, target audience`. `If neither need is degraded, omit the prefix.`

   Then: `Return the GTM plan inside clear delimiters:` followed by this fenced block (a single level of triple-backtick fencing, written literally into the SKILL.md body — do not nest it inside another fence):

   ```
   ─────────────────────────────────────────────────────────────────
   ## Go-to-Market Plan: [Launch Name]
   ─────────────────────────────────────────────────────────────────

   [Generated GTM plan here]

   ─────────────────────────────────────────────────────────────────
   ```

8. **Step 6.5** (`## Step 6.5: Offer to save as brief.md`): state verbatim: `This is a Could-priority by-product (FR-072) — the GTM plan's key messages and channel mix, packaged the same way cc-concept-campaign-concept packages a campaign brief.` Then include these exact sub-steps:

   1. Check if `brief.md` exists in the working directory (the project root — not under `context/`). Run `ls brief.md` from `$PWD`.
   2. If it exists: read it, extract the campaign name (or first heading) and the file's last-modified timestamp, and show both to the user. Ask: overwrite / save under a different name / cancel.
   3. If the user chooses **save under a different name**: ask for a filename (or propose one derived from the launch name), write to that filename instead, and do not touch the existing `brief.md`.
   4. If the user chooses **overwrite** or if no `brief.md` exists: write directly to `brief.md`, covering the launch's key messages and channel mix.

   State verbatim: `Do **not** register brief.md in the ## Context files table in CLAUDE.md — it is a handoff artifact, not persistent context, the same rule cc-concept-campaign-concept follows.`

9. **Step 7** (`## Step 7: Feedback`) per contract: store learnings tagged `[cc-concept:cc-concept-gtm]`. Include these two example entries verbatim:

   ```
   [cc-concept:cc-concept-gtm] client's feature-release launches skip the audience-redefinition step entirely, existing segments always apply — 2026-07-19
   [cc-concept:cc-concept-gtm] client wants milestone dates expressed as week-of-launch offsets (T-4, T-2, T0) rather than calendar dates — 2026-07-19
   ```

- [ ] **Step 3: Verify frontmatter and the gating/framework/milestone/brief.md markers**

Run:

```bash
f=plugins/cc-concept/skills/cc-concept-gtm/SKILL.md
python3 - "$f" <<'PY'
import sys, yaml
meta = yaml.safe_load(open(sys.argv[1]).read().split('---')[1])
assert meta['name'] == 'cc-concept-gtm', meta.get('name')
assert 'allowed-tools' in meta
assert '--type' in meta.get('argument-hint', '')
print("frontmatter OK")
PY
grep -q 'skill-contract.md' "$f" && echo "contract ref OK"
grep -q 'campaign-frameworks.md' "$f" && grep -q -i 'SOSTAC' "$f" && grep -q -i 'RACE' "$f" && grep -q -i 'Message House' "$f" && echo "frameworks named OK"
grep -q -i 'business goals' "$f" && grep -q -i 'target audience' "$f" && echo "two needs OK"
grep -q -i 'DEGRADED' "$f" && grep -q -i 'once' "$f" && echo "three-state OK"
grep -q -i 'DEGRADED OUTPUT — generated without' "$f" && echo "degraded-output prefix OK"
grep -q -i 'at least three' "$f" && grep -q -i 'milestone' "$f" && echo "milestone count OK"
grep -q -i 'product-launch' "$f" && grep -q -i 'feature-release' "$f" && grep -q -i 'market-expansion' "$f" && echo "launch types OK"
grep -q -i 'brief\.md' "$f" && grep -q -i 'overwrite' "$f" && grep -q -i 'different name\|save.as\|save under' "$f" && grep -q -i 'cancel' "$f" && echo "brief.md collision-check OK"
grep -q -i 'not.*regist\|do not register' "$f" && echo "no-context-registration OK"
```

Expected: `frontmatter OK`, `contract ref OK`, `frameworks named OK`, `two needs OK`, `three-state OK`, `degraded-output prefix OK`, `milestone count OK`, `launch types OK`, `brief.md collision-check OK`, `no-context-registration OK`.

- [ ] **Step 4: Commit**

```bash
git add plugins/cc-concept/skills/cc-concept-gtm/SKILL.md
git commit -m ":sparkles: feat(cc-concept): add GTM skill"
```

---

## Task 3: CLAUDE.md registration & fixture verification

Deliverable: both new SKILL.md files are registered in `CLAUDE.md`'s Key Config Files table with real descriptions (no TODO placeholder), and the four verification scenarios from spec §5 pass with the skills invoked for real.

**Files:**

- Modify: `CLAUDE.md` (table rows added by the pre-commit sync hook; pre-populate the descriptions before committing so the hook preserves them instead of writing a TODO)
- Reference: spec §5

**Interfaces:**

- Consumes: both files committed in Tasks 1–2.

- [ ] **Step 1: Pre-populate the CLAUDE.md rows before the sync hook runs**

Open `CLAUDE.md`, find the `## Key Config Files` table, and add these two rows (matching the table's existing column alignment — `prettier` will realign it):

```markdown
| `plugins/cc-concept/skills/cc-concept-content-strategy/SKILL.md` | Skill: Produce a content strategy (pillars, topic clusters, mix, cadence) and register it as context |
| `plugins/cc-concept/skills/cc-concept-gtm/SKILL.md` | Skill: Structure a go-to-market launch plan with an optional brief.md by-product |
```

- [ ] **Step 2: Commit — verify no TODO rows remain**

```bash
git add CLAUDE.md
git commit -m ":memo: docs(cc-concept): register planning skills in CLAUDE.md"
grep -c 'TODO: add description' CLAUDE.md || echo "0 TODO rows OK"
```

Expected: the pre-commit hook's `sync-config-table` output reports either "no changes" or an update that preserves your descriptions (not `TODO: add description` on either new row); `0 TODO rows OK` printed after commit.

- [ ] **Step 3: Fixture A — content strategy, funnel confirmation (proves FR-061)**

Manual, human-in-the-loop. In a project with business goals and target audience loaded, invoke `/cc-concept-content-strategy`.
Expected: a one-line inference summary (audience · goal · funnel focus) is shown and the skill waits for user confirmation or correction before drafting the pillars/mix/cadence.
Fails if: the skill drafts the strategy without ever presenting the inference summary or waiting for confirmation.

- [ ] **Step 4: Fixture B — content strategy registration (proves FR-062)**

Manual. Complete a `/cc-concept-content-strategy` run and accept the save offer.
Expected: a new context file is written (collision-checked), and a row is added to the `## Context files` table with a Summary explicitly naming "content strategy," "pillars," and "topic clusters."
Fails if: the file isn't registered, or the Summary is generic enough that a `cc-content-blog-article` run wouldn't semantically match it.

- [ ] **Step 5: Fixture C — GTM launch-type argument (proves FR-071)**

Manual. Invoke `/cc-concept-gtm --type feature-release`.
Expected: the skill skips the launch-type inference question, states it is using the feature-release type, and the resulting plan is visibly lighter (assumes existing audience/positioning) than a product-launch run would be.
Fails if: it still asks which launch type to use, or the output shows no depth difference from a product-launch run.

- [ ] **Step 6: Fixture D — GTM brief.md by-product (proves FR-072)**

Manual. Complete a `/cc-concept-gtm` run through to the save offer, in a project with an existing `brief.md` (from a prior run or created manually with a distinct name).
Expected: the skill shows the existing file's name and last-modified time before asking overwrite / save-as / cancel — identical behavior to `cc-concept-campaign-concept`'s Fixture D from Slice 2.
Fails if: it overwrites `brief.md` without asking, or fails to show what it would be replacing.

- [ ] **Step 7: Record fixture results**

After running Steps 3–6, note pass/fail for each in the session summary. Any failure is a defect in Task 1 or Task 2's skill file — fix there and re-run, do not paper over in the plan.

---
