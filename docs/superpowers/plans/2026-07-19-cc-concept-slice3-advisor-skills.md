# cc-concept Slice 3 (Advisor Skills) Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add the `cc-concept-marketing-advisor` and `cc-concept-channel-advisor` skills to the existing `cc-concept` plugin — an open-ended strategic Q&A skill with cross-skill deferral, and a structured channel-mix recommendation skill built on the existing RACE framework.

**Architecture:** Two new Markdown files under the existing `cc-concept` plugin repo (`plugins/cc-concept/skills/`), following the same shape as Slices 1–2's skills. No new `_shared/` file — channel-advisor references the existing `_shared/campaign-frameworks.md` directly. No new infra, no new plugin registration. There is no compiled code and no unit-test runner; "tests" are structural assertions (`grep`, `python3` YAML parse) plus a final round of manual fixture runs (spec §5).

**Tech Stack:** Markdown (skill files), `prettier` (repo's PostToolUse formatter), `python3` (frontmatter/YAML validity checks), `gitleaks` (pre-commit secret scan).

## Global Constraints

- **Design source of truth:** `docs/superpowers/specs/2026-07-19-cc-concept-slice3-advisor-skills-design.md`. Every task traces to it.
- **Repo layout standard:** `marketplace/docs/cc-plugin-repo-guideline.md` — do not deviate.
- **Plugin name:** `cc-concept` (already scaffolded). Skills invoked by bare name (`/cc-concept-marketing-advisor`, `/cc-concept-channel-advisor`), never namespaced.
- **No secrets** committed. **No `--force`** flags. Fix root causes.
- **Do not copy skill/plugin files between repos.**
- **Learnings tag formats:** `[cc-concept:cc-concept-marketing-advisor] <observation> — <YYYY-MM-DD>` and `[cc-concept:cc-concept-channel-advisor] <observation> — <YYYY-MM-DD>`.
- **Context model:** free-form `## Context files` table (`| Label | File | Summary |`); skills match on the **Summary** column semantically, never on label or filename.
- **Marketing advisor gates on nothing** (this slice's OQ-007 resolution for this skill) — all context is used silently if present; gaps are noted inline in the answer, never via ask-once/DEGRADED ceremony.
- **Channel advisor gated needs** (this slice's OQ-007 resolution for this skill): exactly two — **business goals** and **target audience** — three-state model (covered / absent-but-supplied-ask-once / absent-and-unanswered-degraded), evaluated independently, same pattern as `cc-concept-campaign-concept`. Current channels and budget are noted silently if present and never block.
- **Marketing advisor deferral list** (FR-042, this slice's OQ-006 resolution): `cc-concept-channel-advisor`, `cc-concept-positioning`, `cc-concept-campaign-concept` always considered; `cc-content-ideation` and `cc-content-text` considered **only if those skills are available in the current session's toolset** — never assumed installed.
- **Marketing advisor output shape** (this slice's OQ-005 resolution): conversational prose sized to the question, still wrapped in the NFR-030 delimiter block with a topic header — no fixed document template.
- **Marketing advisor save-prompt timing** (FR-041): fires after each reply that surfaces a decision, direction, or constraint worth keeping — not once at an explicit "session end" the conversation may never reach. Offers a `.claude/learnings.md` entry or a **new**, collision-checked context file (never edits an existing file it did not create).
- **Channel advisor framework:** RACE only, from `plugins/cc-concept/skills/_shared/campaign-frameworks.md` — no new framework file.
- **Channel advisor degraded-output prefix:** matches the fix applied to `cc-concept-campaign-concept` in Slice 2 — `⚠ DEGRADED OUTPUT — generated without: <needs>` prefixed before the delimiter block when Step 2 lands in the degraded state for either or both gated needs; omitted otherwise.

---

## File Structure

| Path                                                              | Responsibility                                                       |
| ----------------------------------------------------------------- | -------------------------------------------------------------------- |
| `plugins/cc-concept/skills/cc-concept-marketing-advisor/SKILL.md` | Open-ended strategic Q&A, cross-skill deferral, per-turn save-prompt |
| `plugins/cc-concept/skills/cc-concept-channel-advisor/SKILL.md`   | RACE-based channel-mix recommendation, gated on goals + audience     |
| `CLAUDE.md`                                                       | +2 rows in the Key Config Files table for the two new SKILL.md files |

Already present: `docs/superpowers/specs/2026-07-19-cc-concept-slice3-advisor-skills-design.md`, this plan file, `_shared/skill-contract.md`, `_shared/campaign-frameworks.md`, `_shared/positioning-frameworks.md` (all Slices 1–2, unmodified), `cc-concept-onboarding/SKILL.md`, `cc-concept-positioning/SKILL.md`, `cc-concept-campaign-concept/SKILL.md` (all Slices 1–2, unmodified).

---

## Task 1: Marketing advisor skill

Deliverable: `cc-concept-marketing-advisor/SKILL.md` — a conversational, multi-turn strategic advisor that defers to more specific skills when a question matches one, and offers to persist decisions after each qualifying reply (spec §2).

**Files:**

- Create: `plugins/cc-concept/skills/cc-concept-marketing-advisor/SKILL.md`
- Depends on: `_shared/skill-contract.md` (Slice 1)
- Reference (read for shape, do not modify): `plugins/cc-concept/skills/cc-concept-positioning/SKILL.md` (for the collision-check pattern used in the save-prompt)

**Interfaces:**

- Consumes: the `## Context files` table (no fixed need list); the shared contract.
- Produces: optional new context files under `context/` (collision-checked, registered in the `## Context files` table), optional `.claude/learnings.md` entries tagged `[cc-concept:cc-concept-marketing-advisor]`.

- [ ] **Step 1: Write the SKILL.md frontmatter**

```markdown
---
name: cc-concept-marketing-advisor
description: >
  Use this skill for open-ended strategic marketing, sales, or product-market questions
  that don't fit a templated cc-concept skill. Invoke when the user asks "help me think
  through...", wants marketing advice on a topic, or raises a strategic question without
  naming a specific campaign, positioning, or channel task. Conducts a structured
  strategic conversation, defers to more specific skills when a question matches one,
  and offers to save decisions as learnings or new context files.
allowed-tools: Read, Write, Edit, Bash
argument-hint: "[strategic question or topic]"
---
```

- [ ] **Step 2: Write the skill body**

Body must contain, in order:

1. Intro (H1 `# Marketing Advisor Skill`, then a short paragraph): this skill conducts an open-ended strategic conversation on marketing, sales, or product-market topics, deferring to more specific `cc-concept` (and, when available, `cc-content`) skills rather than duplicating their work.
2. **Contract reference:** `This skill follows the shared step sequence in ../_shared/skill-contract.md. Steps below add only marketing-advisor-specific behavior — this is a conversational, multi-turn skill, so Steps 3–7 re-run on each substantive question within the same invocation rather than firing once.`
3. **Step 0–1** (`## Step 0–1: Recall learnings and load context`): recall learnings silently per the contract. Load the `## Context files` table by Summary. State explicitly: `This skill has no fixed list of required context needs — relevant context varies by question. Load and reference whatever is loaded when it is relevant to the specific question being answered.`
4. **Step 2** (`## Step 2: Gating — none`): state verbatim: `This skill gates on nothing. It never asks an ask-once question and never labels a section ⚠ DEGRADED. When a specific answer would clearly benefit from a context need that isn't loaded, note the gap inline in that answer instead — for example: "I don't have your business goals on file, so this leans generic; happy to sharpen it if you share them."`
5. **Step 3** (`## Step 3: Deferral check`): before answering, check whether the question falls squarely within a more specific skill's scope. Include this exact list:

   ```markdown
   - `cc-concept-channel-advisor` — channel mix or tactics questions
   - `cc-concept-positioning` — differentiation or value-proposition questions
   - `cc-concept-campaign-concept` — full campaign planning questions
   - `cc-content-ideation` — content angle/inspiration questions (only if available in the current session's toolset)
   - `cc-content-text` — drafting a specific piece of content (only if available in the current session's toolset)
   ```

   Then this exact paragraph: `The two cc-content-* deferrals apply only if those skills are available in the current session's toolset (i.e. cc-content is installed) — never assume they exist. If a match is found, name the specific skill and suggest invoking it instead of answering inline. If the user says "answer anyway" (or similar), proceed with an inline answer regardless.`

6. **Step 4** (`## Step 4: Generate`): `Produce a conversational, strategically-grounded answer sized to the question — no fixed section skeleton. Reference loaded context by name when it informed the answer (e.g. "Given your positioning around cost-of-ownership...").`
7. **Step 5–6** (`## Step 5–6: Quality check and delimited output`) per contract: internal quality check (clarity, groundedness, no fabricated specifics), then this exact instruction: `Every reply — even a short one — is wrapped in the delimiter block with a topic header, per NFR-030:`

   ```
   ─────────────────────────────────────────────────────────────────
   ## [Topic Header]
   ─────────────────────────────────────────────────────────────────

   [Conversational answer here]

   ─────────────────────────────────────────────────────────────────
   ```

8. **Step 7** (`## Step 7: Save-prompt`): state verbatim: `After each reply that surfaces a decision, direction, or constraint worth keeping, offer to persist it — do not wait for an explicit "end session" signal that an open-ended conversation may never reach.` Then include these exact sub-steps:

   ```markdown
   1. Ask: "Worth saving this? I can add it to `.claude/learnings.md` (lightweight, for future sessions to recall) or save it as a new context file (for skills to load and reference directly). Which, or neither?"
   2. If **learnings**: append to `.claude/learnings.md` tagged `[cc-concept:cc-concept-marketing-advisor]`.
   3. If **new context file**: derive a short slug from the decision's topic (e.g. "pricing-strategy" from a pricing decision). Write to `context/advisor-<slug>.md`. **Apply collision-check logic**: if that filename already exists, append a `-N` suffix before `.md` (try `-2`, then `-3`, etc.) until a filename that does not already exist is found. Never overwrite an existing file. Confirm the file was created, then add a row to the `## Context files` table in `CLAUDE.md` with a Summary that semantically describes the saved decision.
   4. If **neither**: continue without saving.

   This skill never edits an existing context file it did not create.
   ```

   Then two verbatim example learnings entries:

   ```
   [cc-concept:cc-concept-marketing-advisor] client decided to deprioritize enterprise segment for the next two quarters, focus on SMB — 2026-07-19
   [cc-concept:cc-concept-marketing-advisor] client rejected a rebrand discussion as out of scope for this engagement — 2026-07-19
   ```

- [ ] **Step 3: Verify frontmatter and the gating/deferral/save-prompt markers**

Run:

```bash
f=plugins/cc-concept/skills/cc-concept-marketing-advisor/SKILL.md
python3 - "$f" <<'PY'
import sys, yaml
meta = yaml.safe_load(open(sys.argv[1]).read().split('---')[1])
assert meta['name'] == 'cc-concept-marketing-advisor', meta.get('name')
assert 'allowed-tools' in meta
print("frontmatter OK")
PY
grep -q 'skill-contract.md' "$f" && echo "contract ref OK"
grep -q -i 'gates on nothing' "$f" && echo "no-gating OK"
grep -q 'cc-concept-channel-advisor' "$f" && grep -q 'cc-concept-positioning' "$f" && grep -q 'cc-concept-campaign-concept' "$f" && echo "in-plugin deferral OK"
grep -q 'cc-content-ideation' "$f" && grep -q 'cc-content-text' "$f" && grep -q -i 'available in the current session' "$f" && echo "cross-plugin deferral OK"
grep -q -i 'answer anyway' "$f" && echo "override phrase OK"
grep -q -i 'DEGRADED OUTPUT' "$f" || echo "no-degraded-output-prefix OK (expected absent)"
grep -q -i 'delimiter block with a topic header' "$f" && echo "delimited-output-per-turn OK"
grep -q -i 'worth saving this' "$f" && grep -q -i 'collision-check' "$f" && echo "save-prompt OK"
```

Expected: `frontmatter OK`, `contract ref OK`, `no-gating OK`, `in-plugin deferral OK`, `cross-plugin deferral OK`, `override phrase OK`, `no-degraded-output-prefix OK (expected absent)`, `delimited-output-per-turn OK`, `save-prompt OK`.

- [ ] **Step 4: Commit**

```bash
git add plugins/cc-concept/skills/cc-concept-marketing-advisor/SKILL.md
git commit -m ":sparkles: feat(cc-concept): add marketing advisor skill"
```

---

## Task 2: Channel advisor skill

Deliverable: `cc-concept-channel-advisor/SKILL.md` — a RACE-based channel-mix recommendation skill, gated on business goals and target audience with the three-state model (spec §3).

**Files:**

- Create: `plugins/cc-concept/skills/cc-concept-channel-advisor/SKILL.md`
- Depends on: `_shared/skill-contract.md` (Slice 1), `_shared/campaign-frameworks.md` (Slice 2, RACE section)

**Interfaces:**

- Consumes: the `## Context files` table (business goals + target audience Summaries, plus current channels and budget if present); `../_shared/campaign-frameworks.md`'s RACE section; the shared contract.
- Produces: a delimited channel recommendation; no file writes.

- [ ] **Step 1: Write the SKILL.md frontmatter**

```markdown
---
name: cc-concept-channel-advisor
description: >
  Use this skill to recommend a channel mix and tactics for a specific marketing goal,
  audience, and budget context. Invoke when the user asks to "recommend a channel mix",
  "which channels should we use", or wants a channel strategy for a goal or campaign.
  Produces recommended primary and supporting channels, tactical recommendations, and
  flags prerequisites the user may be missing.
allowed-tools: Read, Write, Edit, Bash
argument-hint: "[optional: goal or campaign this recommendation is for]"
---
```

- [ ] **Step 2: Write the skill body**

Body must contain, in order:

1. Intro (H1 `# Channel Advisor Skill`, then a short paragraph): this skill recommends a channel mix and tactics for a specific goal, audience, and budget context, sequenced against the RACE funnel model.
2. **Contract reference:** `This skill follows the shared step sequence in ../_shared/skill-contract.md. Steps below add only channel-advisor-specific behavior.`
3. **Step 0–1** (`## Step 0–1: Recall learnings and load context`): recall learnings silently. Load the `## Context files` table by Summary. State explicitly: look for **business goals/KPIs** and **target audience** (the two gated needs); note silently if present, never ask about: current marketing channels, budget.
4. **Step 2** (`## Step 2: Gating — Three-State Model`): gate on **exactly two** needs — **business goals** and **target audience**. For each, resolve one of three states — **covered** (use silently, no ask), **absent-but-supplied** (ask once, user answers → use, non-degraded), **absent-and-unanswered** (asked once, no usable answer → that section labelled **⚠ DEGRADED**, never fabricated, rest still generates).

   **Check business goals.** Search the context table Summary column for semantic matches: business goals, KPIs, objectives, targets, growth stage, success metrics. If covered, use silently. If absent, ask once:

   > "I need to understand what this channel recommendation should achieve. Briefly: What are your primary business goals or KPIs right now? (e.g. revenue growth, lead volume, retention, brand awareness) Is there a specific target or metric this recommendation should support?"

   If the user provides a usable answer, proceed non-degraded. If they decline or the answer is too vague to use, label the section `## Business Goals ⚠ DEGRADED` in the output and continue.

   **Check target audience.** Search the context table Summary column for semantic matches: target audience, positioning, organization background, customer segments, buyer profile. Prefer a `cc-concept-positioning` output file's Summary if one is registered; else fall back to organization background. If covered, use silently. If absent, ask once:

   > "I need to understand who this channel recommendation is for. Briefly: Who is the target audience? (role, company type/size if B2B, or demographic if B2C) What stage are they typically at when they encounter you? (just learning you exist, actively comparing options, or already a customer)"

   If the user provides a usable answer, proceed non-degraded. If they decline or the answer is too vague to use, label the section `## Target Audience ⚠ DEGRADED` in the output and continue.

5. **Step 3** (`## Step 3: Calibrate`): `Take the goal from $ARGUMENTS if given, else from loaded business goals or the Step 2 gating answer. No campaign-type inference is needed here — just goal, audience, and whatever current-channel/budget context is loaded.`
6. **Step 4** (`## Step 4: Generate`): apply RACE from `../_shared/campaign-frameworks.md`. **State the mapping being applied** before generating. Example:

   > "Using RACE to sequence channels by funnel stage."

   Produce a channel recommendation that includes:

   - **Primary channel(s)** — with rationale tied to the loaded goal and audience.
   - **Supporting channel(s)** — channels that reinforce the primary channel(s).
   - **Tactical recommendations** — at least one concrete tactic per recommended channel.
   - **Existing-channel calls** — for each recommended channel, a maintain/grow/reduce/exit call **if** current channels were loaded; omit this element entirely if no current-channels context is loaded.
   - **Prerequisites** — for any recommended channel where the loaded context suggests it may be out of reach (budget, capability, or skills the user may not have), a "prerequisites" note naming what's missing.

7. **Step 5–6** (`## Step 5–6: Quality check and delimited output`) per contract: the quality check must explicitly verify all five elements above are present (existing-channel calls only when current-channels context was loaded). Then this exact instruction, matching the mechanic already shipped in `cc-concept-campaign-concept`:

   State: `If Step 2 ended in a degraded state for one or both gated needs (business goals and/or target audience), prefix the output with:` followed by a one-line code span `⚠ DEGRADED OUTPUT — generated without: <comma-separated list of unmet needs>`.

   Then state: `For example, if target audience is degraded but business goals are not, prefix with:` followed by the code span `⚠ DEGRADED OUTPUT — generated without: target audience`. `If both are degraded, prefix with:` followed by the code span `⚠ DEGRADED OUTPUT — generated without: business goals, target audience`. `If neither need is degraded, omit the prefix.`

   Then: `Return the channel recommendation inside clear delimiters:` followed by this fenced block (a single level of triple-backtick fencing, written literally into the SKILL.md body — do not nest it inside another fence):

   ```
   ─────────────────────────────────────────────────────────────────
   ## Channel Recommendation
   ─────────────────────────────────────────────────────────────────

   [Generated channel recommendation here]

   ─────────────────────────────────────────────────────────────────
   ```

8. **Step 7** (`## Step 7: Feedback`) per contract: store learnings tagged `[cc-concept:cc-concept-channel-advisor]`. Include these two example entries verbatim:

   ```
   [cc-concept:cc-concept-channel-advisor] client vetoed paid social entirely, treat as excluded from all future recommendations — 2026-07-19
   [cc-concept:cc-concept-channel-advisor] client's existing email list is small (<500) and shouldn't be weighted as a primary channel yet — 2026-07-19
   ```

- [ ] **Step 3: Verify frontmatter and the gating/framework/degradation markers**

Run:

```bash
f=plugins/cc-concept/skills/cc-concept-channel-advisor/SKILL.md
python3 - "$f" <<'PY'
import sys, yaml
meta = yaml.safe_load(open(sys.argv[1]).read().split('---')[1])
assert meta['name'] == 'cc-concept-channel-advisor', meta.get('name')
assert 'allowed-tools' in meta
print("frontmatter OK")
PY
grep -q 'skill-contract.md' "$f" && echo "contract ref OK"
grep -q 'campaign-frameworks.md' "$f" && grep -q -i 'RACE' "$f" && echo "framework ref OK"
grep -q -i 'business goals' "$f" && grep -q -i 'target audience' "$f" && echo "two needs OK"
grep -q -i 'DEGRADED' "$f" && grep -q -i 'once' "$f" && echo "three-state OK"
grep -q -i 'DEGRADED OUTPUT — generated without' "$f" && echo "degraded-output prefix OK"
grep -q -i 'prerequisites' "$f" && echo "prerequisites OK"
grep -q -i 'maintain/grow/reduce/exit\|maintain, grow, reduce, exit\|maintain/grow/reduce/exit call' "$f" && echo "existing-channel call OK"
```

Expected: `frontmatter OK`, `contract ref OK`, `framework ref OK`, `two needs OK`, `three-state OK`, `degraded-output prefix OK`, `prerequisites OK`, `existing-channel call OK`.

- [ ] **Step 4: Commit**

```bash
git add plugins/cc-concept/skills/cc-concept-channel-advisor/SKILL.md
git commit -m ":sparkles: feat(cc-concept): add channel advisor skill"
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
| `plugins/cc-concept/skills/cc-concept-marketing-advisor/SKILL.md` | Skill: Open-ended strategic advisor with cross-skill deferral and per-turn save-prompt |
| `plugins/cc-concept/skills/cc-concept-channel-advisor/SKILL.md` | Skill: Recommend a RACE-sequenced channel mix for a goal, audience, and budget |
```

- [ ] **Step 2: Commit — verify no TODO rows remain**

```bash
git add CLAUDE.md
git commit -m ":memo: docs(cc-concept): register advisor skills in CLAUDE.md"
grep -c 'TODO: add description' CLAUDE.md || echo "0 TODO rows OK"
```

Expected: the pre-commit hook's `sync-config-table` output reports either "no changes" or an update that preserves your descriptions (not `TODO: add description` on either new row); `0 TODO rows OK` printed after commit.

- [ ] **Step 3: Fixture A — deferral (proves FR-042, this slice's OQ-006 resolution)**

Manual, human-in-the-loop. Invoke `/cc-concept-marketing-advisor` and ask a channel-mix-shaped question (e.g. "what channels should we focus on?").
Expected: the skill names `cc-concept-channel-advisor` and suggests invoking it instead of answering inline. If you then say "answer anyway," it proceeds with an inline answer.
Fails if: it refuses to answer even after "answer anyway," or it answers inline without ever naming the more specific skill.

- [ ] **Step 4: Fixture B — advisor save-prompt (proves FR-041)**

Manual. In the same session, ask `/cc-concept-marketing-advisor` an open strategic question that surfaces a clear decision (e.g. "should we deprioritize our enterprise segment for now?").
Expected: the reply is delimited and headed per NFR-030, and ends with an offer to save the decision — either to `.claude/learnings.md` or as a new context file — not a generic "let me know if you want anything else."
Fails if: the reply never offers to save anything, or the offer only appears after an explicit "end session" cue rather than after the qualifying reply itself.

- [ ] **Step 5: Fixture C — channel advisor, bare project (proves NFR-041, NFR-011, this slice's OQ-007 resolution)**

Manual. In a fresh scratch project with no context, invoke `/cc-concept-channel-advisor`.
Expected: both business goals and target audience hit the ask-once/degrade path; current channels and budget are never asked about. If given no usable answer for either, the output carries the `⚠ DEGRADED OUTPUT` prefix and both sections are labelled `⚠ DEGRADED`.
Fails if: it asks more than once per need, asks about current channels or budget, or fabricates content instead of degrading.

- [ ] **Step 6: Fixture D — channel advisor, current channels loaded (proves FR-051)**

Manual. In a project with a context file describing existing marketing channels (e.g. "we currently run email and organic LinkedIn"), invoke `/cc-concept-channel-advisor`.
Expected: the recommendation explicitly calls out a maintain/grow/reduce/exit decision for each existing channel mentioned in that context file.
Fails if: the recommendation ignores the existing channels or fails to make an explicit call for any of them.

- [ ] **Step 7: Record fixture results**

After running Steps 3–6, note pass/fail for each in the session summary. Any failure is a defect in Task 1 or Task 2's skill file — fix there and re-run, do not paper over in the plan.

---
