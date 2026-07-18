# cc-concept Slice 2 (Campaign Concept Skill) Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add the `cc-concept-campaign-concept` skill and its framework library to the existing `cc-concept` plugin, closing the strategy-to-content loop with a `brief.md` handoff `cc-content` skills can consume directly.

**Architecture:** Two new Markdown files under the existing `cc-concept` plugin repo (`plugins/cc-concept/skills/`), following the same shape as Slice 1's positioning skill and framework library. No new infra, no new plugin registration — `cc-concept` is already scaffolded and cataloged. There is no compiled code and no unit-test runner; "tests" are structural assertions (`bash -n`, YAML parse, `grep` for required sections) plus a final round of manual fixture runs (spec §7).

**Tech Stack:** Markdown (skill + shared reference file), `prettier` (already the repo's PostToolUse formatter), `python3` (frontmatter/YAML validity checks), `gitleaks` (pre-commit secret scan, already active from Slice 1).

## Global Constraints

- **Design source of truth:** `docs/superpowers/specs/2026-07-18-cc-concept-slice2-campaign-concept-design.md`. Every task traces to it.
- **Repo layout standard:** `marketplace/docs/cc-plugin-repo-guideline.md` — do not deviate.
- **Plugin name:** `cc-concept` (already scaffolded). Skill invoked by bare name (`/cc-concept-campaign-concept`), never namespaced.
- **No secrets** committed. **No `--force`** flags. Fix root causes.
- **Do not copy skill/plugin files between repos** — the marketplace references `cc-concept` via `git-subdir`; no marketplace change is needed this slice (the plugin is already cataloged, only a new skill file inside it).
- **Learnings tag format:** `[cc-concept:cc-concept-campaign-concept] <observation> — <YYYY-MM-DD>`.
- **Context model:** free-form `## Context files` table (`| Label | File | Summary |`); skills match on the **Summary** column semantically, never on label or filename.
- **Gated needs (this slice's OQ-007 resolution):** exactly two — **business goals** and **target audience** — three-state model (covered / absent-but-supplied-ask-once / absent-and-unanswered-degraded), evaluated independently. Everything else (competitive landscape, current channels, growth stage, brand-specific strategy overrides) is noted silently if present and never blocks.
- **Campaign types (FR-033):** `product-launch`, `thought-leadership`, `seasonal-promotion`, `retention`, `lead-generation`, `brand-awareness`.
- **brief.md location:** working-directory root, never under `context/`. **Not** registered in the `## Context files` table (it is a handoff artifact, not persistent context — see spec §4.4).
- **brief.md collision handling (NFR-040):** never overwrite silently — show the existing file's campaign name + last-modified, then offer overwrite / save-as / cancel.
- **Framework composition model:** SOSTAC, RACE, and Message House are **not** alternatives to pick between — all three are applied on every run, each governing a specific output facet (spec §3). Do not write a "pick one" selection process for this file.

---

## File Structure

| Path                                                             | Responsibility                                                                     |
| ---------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| `plugins/cc-concept/skills/_shared/campaign-frameworks.md`       | SOSTAC + RACE + Message House, composable-by-facet, plus the project-override rule |
| `plugins/cc-concept/skills/cc-concept-campaign-concept/SKILL.md` | Campaign concept generation + `brief.md` handoff                                   |
| `CLAUDE.md`                                                      | +1 row in the Key Config Files table for the new SKILL.md                          |

Already present: `docs/superpowers/specs/2026-07-18-cc-concept-slice2-campaign-concept-design.md`, this plan file, `_shared/skill-contract.md` (Slice 1), `_shared/positioning-frameworks.md` (Slice 1, unmodified), `cc-concept-onboarding/SKILL.md` and `cc-concept-positioning/SKILL.md` (Slice 1, unmodified).

---

## Task 1: Campaign framework library

Deliverable: `_shared/campaign-frameworks.md` — SOSTAC, RACE, and Message House, each mapped to a specific output facet, plus the project-override rule (spec §3).

**Files:**

- Create: `plugins/cc-concept/skills/_shared/campaign-frameworks.md`
- Reference (read for shape, do not modify): `plugins/cc-concept/skills/_shared/positioning-frameworks.md`

**Interfaces:**

- Produces: the reference `cc-concept-campaign-concept` (Task 2) applies in its Step 4 (Generate). The skill states which framework governs which section, per this file's facet mapping.

- [ ] **Step 1: Read the shape reference**

Run:

```bash
cd /home/michael/Git-Repos/clever-cc-plugins/cc-concept
sed -n '1,30p' plugins/cc-concept/skills/_shared/positioning-frameworks.md
```

Expected: shows the framing intro, a "How to select" process, and the per-framework entry shape. This file's structure differs at the "selection" step (facet mapping, not pick-one) but otherwise mirrors this shape.

- [ ] **Step 2: Write `_shared/campaign-frameworks.md`**

The file must contain, in order:

1. **Framing intro** — this library is for `cc-concept-campaign-concept`'s output generation; apply it whenever building a full campaign concept.

2. **"How frameworks apply to this skill's output"** — replace positioning's pick-one selection process with an explicit statement that these three frameworks are **composed together on every run**, each governing one facet, plus this exact mapping table:

   ```markdown
   | Framework     | Governs                            | Output section                                                              |
   | ------------- | ---------------------------------- | --------------------------------------------------------------------------- |
   | SOSTAC        | Overall campaign structure         | Campaign name+objective+audience, key messages, channel mix, creative brief |
   | RACE          | Channel sequencing by funnel stage | Channel mix section specifically                                            |
   | Message House | Message architecture               | Key messages section specifically                                           |
   ```

3. **Framework Reference — SOSTAC** (What it is / How it maps to this skill's output / How to apply):

   - What it is: A six-stage campaign planning structure — Situation (current context: audience, market, competitive landscape), Objectives (what the campaign must achieve, tied to business goals), Strategy (the overall approach), Tactics (the specific tools and message architecture), Action (the channel mix and sequencing), Control (how success will be measured, tied back to Objectives).
   - How it maps: Situation + Objectives → campaign name, objective, and target audience summary. Strategy + Tactics → key messages (in conjunction with Message House). Action → channel mix (in conjunction with RACE). Control → the creative brief's success framing.
   - How to apply: (1) Summarize the situation from loaded context. (2) State the objective in outcome terms, tied to loaded business goals. (3) Name the target audience specifically. (4) Hand off to Message House for messaging and RACE for channels. (5) Close with Control: state what "this campaign worked" looks like, in terms the loaded business goals define as success.

4. **Framework Reference — RACE**:

   - What it is: A four-stage funnel model for sequencing marketing activity — Reach (build awareness with a new audience), Act (encourage engagement/consideration), Convert (turn interest into the desired action), Engage (retain and grow the relationship post-conversion).
   - How it maps: applied specifically inside the channel-mix section, sequencing proposed channels against the stages the campaign's funnel stage and type call for.
   - **Campaign-type emphasis** (informs, does not override, the skill's own funnel-stage inference) — include this exact table:

     ```markdown
     | Campaign type                   | RACE emphasis  |
     | ------------------------------- | -------------- |
     | product-launch, brand-awareness | Reach + Act    |
     | lead-generation                 | Act + Convert  |
     | thought-leadership              | Reach + Engage |
     | seasonal-promotion              | Convert        |
     | retention                       | Engage         |
     ```

   - How to apply: (1) Identify which stage(s) the campaign objective and funnel stage most need. (2) For each stage in play, name at least one channel with a rationale grounded in loaded context (current channels, if present). (3) Sequence stages in a rough timeline if the campaign spans multiple phases. (4) Note stages deliberately left light so the omission reads as a decision, not an oversight.

5. **Framework Reference — Message House**:

   - What it is: A message-architecture framework — one **roof statement** (the single core message the whole campaign reinforces), 2–4 **pillars** (supporting messages, each defensible on its own), and **proof points** under each pillar (concrete evidence that makes the pillar believable).
   - How it maps: applied specifically inside the key-messages section. The roof statement anchors the campaign's throughline; each of FR-030's required ≥2 key messages corresponds to one pillar.
   - How to apply: (1) State the roof statement in one sentence. (2) Derive 2–4 pillars that each support the roof statement from a different angle. (3) For each pillar, name at least one proof point grounded in loaded context (positioning output, organization background) rather than asserted generically. (4) Check that no pillar contradicts another.

6. **Project override** — include this rule, adapted from positioning-frameworks.md's override step: _"If loaded context expresses a framework preference or prohibition for campaign planning (e.g. 'never sequence channels with RACE, always use our own funnel model', or 'always structure messaging around Jobs-to-be-Done instead of Message House'), that preference wins over this file's default composition. State the override when it applies; do not edit this file to encode project-specific preferences."_

- [ ] **Step 3: Verify all three frameworks, the facet mapping, and the override rule are present**

Run:

```bash
f=plugins/cc-concept/skills/_shared/campaign-frameworks.md
grep -q -i 'SOSTAC' "$f" && grep -q -i 'RACE' "$f" && grep -q -i 'Message House' "$f" && echo "3 frameworks OK"
grep -q -i 'governs\|facet' "$f" && echo "facet mapping OK"
grep -q -i 'override\|wins over\|preference' "$f" && echo "override rule OK"
grep -q -i 'roof statement' "$f" && grep -q -i 'pillar' "$f" && grep -q -i 'proof point' "$f" && echo "message house structure OK"
grep -q -i 'reach' "$f" && grep -q -i 'engage' "$f" && echo "race stages OK"
```

Expected: `3 frameworks OK`, `facet mapping OK`, `override rule OK`, `message house structure OK`, `race stages OK`.

- [ ] **Step 4: Commit**

```bash
git add plugins/cc-concept/skills/_shared/campaign-frameworks.md
git commit -m ":memo: feat(cc-concept): add campaign framework library"
```

---

## Task 2: Campaign concept skill

Deliverable: `cc-concept-campaign-concept/SKILL.md` — generates a full campaign concept against the framework library, gates on business goals + target audience with the three-state model, and offers a collision-checked `brief.md` handoff (spec §2, §4).

**Files:**

- Create: `plugins/cc-concept/skills/cc-concept-campaign-concept/SKILL.md`
- Depends on: `_shared/skill-contract.md` (Slice 1), `_shared/campaign-frameworks.md` (Task 1)

**Interfaces:**

- Consumes: the `## Context files` table (business goals + target audience Summaries, preferring a `cc-concept-positioning` output file for audience if registered); `_shared/campaign-frameworks.md`; the shared contract.
- Produces: `brief.md` in the working-directory root (collision-checked, **not** registered as context), consumable by `cc-content` skills via `$ARGUMENTS` or `ls brief.md`.

- [ ] **Step 1: Write the SKILL.md frontmatter**

```markdown
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
```

- [ ] **Step 2: Write the skill body**

Body must contain, in order:

1. Intro: this skill turns a campaign objective into a complete campaign concept, and hands the result to `cc-content` as `brief.md`.
2. **Contract reference:** `This skill follows the shared step sequence in ../_shared/skill-contract.md. Steps below add only campaign-concept-specific behavior.`
3. **Step 0–1** per contract (recall learnings; load the `## Context files` table by Summary). State explicitly: look for **business goals/KPIs** and **target audience** (preferring a `cc-concept-positioning` output file if one is registered, else organization background) as the two gated needs; note silently if present, never ask about: competitive landscape, current marketing channels, growth stage, brand-specific strategy overrides.
4. **Step 2 (Gating — three-state model):** Gate on **exactly two** needs — **business goals** and **target audience**. For each, resolve one of three states — **covered** (use silently, no ask), **absent-but-supplied** (ask once, user answers → use, non-degraded), **absent-and-unanswered** (asked once, no usable answer → that section labelled **⚠ DEGRADED**, never fabricated, rest still generates).

   **Check business goals.** Search the context table Summary column for semantic matches: business goals, KPIs, objectives, targets, growth stage, success metrics. If covered, use silently. If absent, ask once:

   > "I need to understand what this campaign should achieve. Briefly: What are your primary business goals or KPIs right now? (e.g. revenue growth, lead volume, retention, brand awareness) Is there a specific target or metric this campaign should move?"

   If the user provides a usable answer, proceed non-degraded. If they decline or the answer is too vague to use, label the section `## Business Goals ⚠ DEGRADED` in the output and continue.

   **Check target audience.** Search the context table Summary column for semantic matches: target audience, positioning, organization background, customer segments, buyer profile. Prefer a `cc-concept-positioning` output file's Summary if one is registered; else fall back to organization background. If covered, use silently. If absent, ask once:

   > "I need to understand who this campaign is for. Briefly: Who is the target audience? (role, company type/size if B2B, or demographic if B2C) What stage are they typically at when they encounter you? (just learning you exist, actively comparing options, or already a customer)"

   If the user provides a usable answer, proceed non-degraded. If they decline or the answer is too vague to use, label the section `## Target Audience ⚠ DEGRADED` in the output and continue.

5. **Step 3 (Calibrate):** If `--type` was passed in `$ARGUMENTS`, use it directly and skip the campaign-type question (FR-033). Otherwise infer campaign type, funnel stage, and B2B/B2C from loaded context (FR-032); where inference isn't confident, ask the missing question directly rather than guessing. Present a one-line inference summary (e.g. `"Type: product launch · Audience: B2B mid-market · Stage: TOFU"`) and wait for user confirmation or correction before drafting.
6. **Step 4 (Generate):** Apply the three frameworks from `../_shared/campaign-frameworks.md` per that file's facet mapping — **state the mapping being applied** before generating (e.g. `"Structuring with SOSTAC; sequencing channels with RACE (retention emphasis); messaging with Message House."`). Produce: campaign name, objective, target audience summary, at least two key messages (one per Message House pillar), proposed channel mix (RACE-sequenced), and a creative brief section (tone/voice notes if brand-voice context is loaded, primary CTA, constraints, suggested formats per channel).
7. **Step 5–6 (Quality check + delimited output)** per contract. The quality check must explicitly verify: all of FR-030's six required elements are present, AND the four `cc-content`-extractable elements (goals, key messages, constraints, CTAs) are present in prose — this second check is what Step 6.5 relies on before offering to save.
8. **Step 6.5 (Offer to save as `brief.md`):**
   - Check if `brief.md` exists in the working directory (`ls brief.md` from `$PWD`, the project root — not under `context/`).
   - If it exists: read it, extract the campaign name (or first heading) and the file's last-modified timestamp, and show both to the user. Ask: overwrite / save under a different name / cancel.
   - If the user chooses save-as: ask for a filename (or propose one derived from the new campaign name), write there instead, and do not touch the existing `brief.md`.
   - If the user chooses overwrite or if no `brief.md` exists: write directly to `brief.md`.
   - **Do not** register `brief.md` in the `## Context files` table — it is a handoff artifact, not persistent context (spec §4.4).
9. **Step 7 (Feedback)** per contract: store learnings tagged `[cc-concept:cc-concept-campaign-concept]`. Include these two example entries verbatim in the SKILL.md body:

   ```
   [cc-concept:cc-concept-campaign-concept] client rejected the inferred "lead-generation" type for a customer-only campaign; retention fits their base better — 2026-07-18
   [cc-concept:cc-concept-campaign-concept] client prefers email + LinkedIn as primary channels, treats paid social as a last resort — 2026-07-18
   ```

- [ ] **Step 3: Verify frontmatter and the gating/degradation/framework/collision markers**

Run:

```bash
f=plugins/cc-concept/skills/cc-concept-campaign-concept/SKILL.md
python3 - "$f" <<'PY'
import sys, yaml
meta = yaml.safe_load(open(sys.argv[1]).read().split('---')[1])
assert meta['name'] == 'cc-concept-campaign-concept', meta.get('name')
assert 'allowed-tools' in meta
assert '--type' in meta.get('argument-hint', '')
print("frontmatter OK")
PY
grep -q 'skill-contract.md' "$f" && echo "contract ref OK"
grep -q 'campaign-frameworks.md' "$f" && echo "library ref OK"
grep -q -i 'business goals' "$f" && grep -q -i 'target audience' "$f" && echo "two needs OK"
grep -q -i 'DEGRADED' "$f" && grep -q -i 'once' "$f" && echo "three-state OK"
grep -q -i 'brief\.md' "$f" && echo "brief.md ref OK"
grep -q -i 'overwrite' "$f" && grep -q -i 'different name\|save.as\|save under' "$f" && grep -q -i 'cancel' "$f" && echo "collision-check OK"
grep -q -i 'not.*regist\|do not register' "$f" && echo "no-context-registration OK"
grep -q -i 'SOSTAC' "$f" && grep -q -i 'RACE' "$f" && grep -q -i 'Message House' "$f" && echo "frameworks named OK"
grep -q -i 'product-launch' "$f" && grep -q -i 'retention' "$f" && echo "campaign types OK"
```

Expected: `frontmatter OK`, `contract ref OK`, `library ref OK`, `two needs OK`, `three-state OK`, `brief.md ref OK`, `collision-check OK`, `no-context-registration OK`, `frameworks named OK`, `campaign types OK`.

- [ ] **Step 4: Commit**

```bash
git add plugins/cc-concept/skills/cc-concept-campaign-concept/SKILL.md
git commit -m ":sparkles: feat(cc-concept): add campaign concept skill"
```

---

## Task 3: CLAUDE.md registration & fixture verification

Deliverable: the new SKILL.md is registered in `CLAUDE.md`'s Key Config Files table with a real description (no TODO placeholder — the lesson from Slice 1's registration churn), and the four verification scenarios from spec §7 pass with the skill invoked for real.

**Files:**

- Modify: `CLAUDE.md` (table row added by the pre-commit sync hook; pre-populate the description before committing so the hook preserves it instead of writing a TODO)
- Reference: spec §7

**Interfaces:**

- Consumes: both files committed in Tasks 1–2.

- [ ] **Step 1: Pre-populate the CLAUDE.md row before the sync hook runs**

The sync hook (`scripts/sync-config-table.sh`) appends a `TODO: add description` row for any new file it discovers that has no existing row — Slice 1 shipped with several of these and they had to be fixed later. Avoid that by adding the row yourself first.

Open `CLAUDE.md`, find the `## Key Config Files` table, and add this row (matching the table's existing column alignment — `prettier` will realign it):

```markdown
| `plugins/cc-concept/skills/cc-concept-campaign-concept/SKILL.md` | Skill: Build a campaign concept and hand it off to cc-content as brief.md |
```

Also add a row for the shared library, since it too is a new file the sync hook will otherwise flag:

```markdown
| `plugins/cc-concept/skills/_shared/campaign-frameworks.md` | Campaign planning frameworks: SOSTAC, RACE, Message House |
```

- [ ] **Step 2: Commit — verify the sync hook reports no TODO rows**

```bash
git add CLAUDE.md
git commit -m ":memo: docs(cc-concept): register campaign-concept skill in CLAUDE.md"
grep -c 'TODO: add description' CLAUDE.md || echo "0 TODO rows OK"
```

Expected: the pre-commit hook's `sync-config-table` output reports either "no changes" or an update that preserves your descriptions (not `TODO: add description` on either new row); `0 TODO rows OK` printed after commit.

- [ ] **Step 3: Fixture A — bare project (proves NFR-041, degradation mechanics)**

Manual, human-in-the-loop. In a fresh scratch project with **no** context (no onboarding, no positioning run), invoke `/cc-concept-campaign-concept`.
Expected: the skill detects both business goals and target audience uncovered, asks once for each, and — if given no usable answer — produces output with both sections labelled `⚠ DEGRADED` and the `⚠ DEGRADED OUTPUT` prefix, without hard-erroring or asking twice for the same need.
Fails if: it asks more than once per need, fabricates content instead of degrading, or refuses to run.

- [ ] **Step 4: Fixture B — onboarded + positioned project (proves context-reuse, positioning-output preference)**

Manual. In a scratch project where `cc-concept-onboarding` and `cc-concept-positioning` have both already run, invoke `/cc-concept-campaign-concept`.
Expected: both gated needs resolve as **covered** with no questions asked — business goals from the onboarding-collected context, target audience from the positioning output file specifically (not a generic org-background guess). The generated campaign's target audience summary should visibly reflect the positioning document's content.
Fails if: it asks for either need despite coverage, or ignores the positioning output in favor of a weaker source.

- [ ] **Step 5: Fixture C — campaign-type argument (proves FR-033)**

Manual. In the same onboarded+positioned project, invoke `/cc-concept-campaign-concept` with `--type retention`.
Expected: the skill skips the campaign-type inference question entirely, states it is using the retention type, and the channel-mix section visibly applies RACE's retention emphasis (Engage-weighted) per the campaign-frameworks.md table.
Fails if: it still asks which campaign type to use, or the channel mix shows no retention-specific emphasis.

- [ ] **Step 6: Fixture D — brief.md collision (proves NFR-040, spec §4.3)**

Manual. In a project with an existing `brief.md` (from a prior run or created manually with a distinct campaign name), invoke `/cc-concept-campaign-concept` and complete a run through to the save offer.
Expected: the skill shows the existing file's campaign name and last-modified time before asking overwrite / save-as / cancel; choosing save-as leaves the original `brief.md` untouched and writes the new campaign to a different filename; choosing overwrite replaces it only after the explicit choice.
Fails if: it overwrites `brief.md` without asking, or fails to show what it would be replacing.

- [ ] **Step 7: Record fixture results**

After running Steps 3–6, note pass/fail for each in the session summary. Any failure is a defect in Task 2's skill file — fix there and re-run, do not paper over in the plan.

---
