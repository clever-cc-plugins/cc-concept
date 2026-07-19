# cc-concept — Slice 4 Design: Planning Skills

**Status:** Approved for implementation
**Date:** 2026-07-19
**Source briefing:** `requirements-cc-concept.md` (v2.1)
**Scope:** Slice 4 of 5 (content strategy + go-to-market)

---

## 1. Purpose and scope

Slice 4 adds the two "planning" skills named in the five-slice decomposition
(Slice 1 design §1.1): **`cc-concept-content-strategy`** (editorial planning
framework, FR-060–062) and **`cc-concept-gtm`** (go-to-market launch
planning, FR-070–072).

**In scope:** both skill files, both referencing the existing
`_shared/skill-contract.md`. Neither needs a new framework file:
content-strategy reuses the Message House pillars model from
`_shared/campaign-frameworks.md` (content pillars ≡ Message House pillars);
GTM reuses SOSTAC + RACE + Message House from the same file — the same
composable-by-facet model `cc-concept-campaign-concept` already applies,
since a product launch is structurally a campaign-concept run extended with
launch-type differentiation and milestones.

**Design decisions:**

- **Gating (OQ-007) for both skills:** business goals + target audience —
  the same pattern established for campaign-concept and channel-advisor, for
  consistency and because both FR-061 and FR-070 depend on exactly those two
  inputs.
- **FR-062 (content-strategy registration):** the output is saved and
  registered as a context file, collision-checked like positioning, with a
  Summary written to be legible to `cc-content-blog-article` and
  `cc-content-linkedin-post` — explicitly naming "content strategy,"
  "pillars," and "topic clusters."
- **FR-072 (GTM's optional brief.md by-product, Could-priority):**
  included — GTM reuses campaign-concept's exact Step 6.5 collision-check
  mechanic to optionally save a `brief.md`, since the mechanic already
  exists and the marginal implementation cost is low.
- **FR-071 (launch type):** `--type product-launch|feature-release|market-expansion`
  argument, the same pattern as campaign-concept's `--type`.

**Out of scope:** Slice 5 (learnings-promotion). No changes to any existing
skill file.

Two new files only:

```
plugins/cc-concept/skills/cc-concept-content-strategy/SKILL.md
plugins/cc-concept/skills/cc-concept-gtm/SKILL.md
```

---

## 2. The skill — `cc-concept-content-strategy`

### 2.1 Frontmatter

`name: cc-concept-content-strategy`. Trigger phrases: "content strategy",
"editorial plan", "content pillars", "topic clusters". No `argument-hint`
beyond an optional focus brief.

### 2.2 Step sequence

References `_shared/skill-contract.md`. One-shot generate-and-done, the same
shape as `cc-concept-positioning` and `cc-concept-campaign-concept`.

**Step 0–1 (contract).** Recall learnings; load the `## Context files` table
by Summary. Looks for: business goals and target audience (the two gated
needs, preferring a `cc-concept-positioning` output file for audience).
Noted silently if present: brand voice, existing content inventory,
competitive landscape.

**Step 2 — Gating (this slice's resolution of OQ-007 for this skill).**
Three-state model on **business goals** and **target audience**, same
pattern as campaign-concept/channel-advisor.

**Step 3 — Calibrate (FR-061).** Infer funnel stage and audience type from
loaded context. Present a one-line inference summary (e.g. `"Audience: B2B
mid-market · Goal: lead generation · Funnel focus: MOFU"`) and wait for user
confirmation or correction before drafting — FR-061's explicit requirement.

**Step 4 — Generate.** Apply Message House from `../_shared/campaign-
frameworks.md` for the pillar structure. **State the choice:**

> "Using Message House for content pillar architecture."

Produce: at least two content pillars (Message House pillars), each with
supporting topic clusters; a recommended content type mix with rationale
tied to funnel stage (e.g. TOFU skews video/social, BOFU skews case
studies/comparisons); a suggested publishing cadence.

**Step 5–6 (contract).** Internal quality check verifies FR-060's three
required elements are present, then delimited output per NFR-030, prefixed
with `⚠ DEGRADED OUTPUT — generated without: <needs>` if Step 2 landed in
the degraded state.

**Step 6.5 — Register output (FR-062).** Offer to save as a new,
collision-checked context file (e.g. `context/content-strategy.md`, same
numbering scheme as positioning). Register in the `## Context files` table
with a Summary written to be legible to `cc-content-blog-article` and
`cc-content-linkedin-post` — must explicitly name "content strategy,"
"pillars," and "topic clusters" so those skills' Summary-matching picks it
up; per FR-062's note, this Summary wording is functionally part of the
requirement, not cosmetic.

**Step 7 (contract).** Two-phase feedback, tagged
`[cc-concept:cc-concept-content-strategy]`.

---

## 3. The skill — `cc-concept-gtm`

### 3.1 Frontmatter

`name: cc-concept-gtm`. Trigger phrases: "go-to-market plan", "GTM plan",
"launch plan", "plan a launch".
`argument-hint: "[--type product-launch|feature-release|market-expansion]"`.

### 3.2 Step sequence

References `_shared/skill-contract.md`. One-shot generate-and-done,
structurally the campaign-concept pattern extended with launch type and
milestones.

**Step 0–1 (contract).** Recall learnings; load the `## Context files` table
by Summary. Looks for: business goals and target audience (the two gated
needs, preferring a `cc-concept-positioning` output file). Noted silently if
present: competitive landscape, current channels, existing positioning
depth.

**Step 2 — Gating (this slice's resolution of OQ-007 for this skill).**
Three-state model on **business goals** and **target audience** — same
pattern as the other three templated skills.

**Step 3 — Calibrate (FR-071).** If `--type` was passed, use it directly and
skip the launch-type question; otherwise infer from context and confirm
before drafting — the same mechanic as campaign-concept's `--type`. The
three types scale output depth: **product-launch** gets full-depth treatment
across all elements; **feature-release** is lighter (assumes existing
audience/positioning, focuses on messaging + milestones); **market-
expansion** emphasizes audience redefinition and channel sequencing for the
new market.

**Step 4 — Generate.** Apply SOSTAC + RACE + Message House from
`../_shared/campaign-frameworks.md`, exactly as campaign-concept does.
**State the mapping being applied** before generating. Produce:

- Target audience definition.
- A positioning statement for the launch — derived from loaded positioning
  context if present, else generated fresh using
  `positioning-frameworks.md`'s selection process.
- Proposed channel sequence with timing (RACE-staged).
- Key messages (Message House pillars).
- At least three launch milestones (tied to the Control/SOSTAC facet).

**Step 5–6 (contract).** Internal quality check verifies FR-070's five
required elements plus the ≥3-milestone minimum, then delimited output per
NFR-030, prefixed with `⚠ DEGRADED OUTPUT — generated without: <needs>` if
Step 2 landed degraded.

**Step 6.5 — Offer to save as `brief.md` (FR-072, Could-priority
by-product).** After the delimited output, offer to also save a
`brief.md`-compatible campaign brief covering the launch's key messages and
channel mix — reusing campaign-concept's exact collision-check mechanic
(overwrite / save-as / cancel) verbatim, including the same "not registered
as context" rule.

**Step 7 (contract).** Two-phase feedback, tagged
`[cc-concept:cc-concept-gtm]`.

---

## 4. File layout and config updates

Two new SKILL.md files (§1). No new `_shared/` file — both reuse
`campaign-frameworks.md` directly. `CLAUDE.md`'s Key Config Files table gets
two new rows, with descriptions pre-populated at creation time (the Task 3
pattern established in Slices 2–3).

---

## 5. Verification

Fixtures to run manually post-implementation (same discipline as prior
slices — written here, executed later):

**Fixture A — content strategy, funnel confirmation.** Invoke
`/cc-concept-content-strategy` with business goals + target audience
loaded. Expected: a one-line inference summary is shown and confirmation is
waited on before the pillars/mix/cadence draft. Proves FR-061.

**Fixture B — content strategy registration.** Complete a run and accept the
save offer. Expected: a new context file is written and registered with a
Summary explicitly naming "content strategy," "pillars," and "topic
clusters." Proves FR-062.

**Fixture C — GTM launch-type argument.** Invoke `/cc-concept-gtm --type
feature-release`. Expected: skips the type-inference question, and output
depth is visibly lighter than a product-launch run (assumes existing
audience/positioning). Proves FR-071.

**Fixture D — GTM brief.md by-product.** Complete a GTM run and accept the
brief.md offer. Expected: collision-check behaves identically to
campaign-concept's (existing file → overwrite/save-as/cancel). Proves
FR-072.

---

## 6. Traceability to the briefing

| Requirement                                   | Where addressed                                     |
| --------------------------------------------- | --------------------------------------------------- |
| FR-060 (content strategy skill + output)      | §2.2 Step 4                                         |
| FR-061 (funnel/audience alignment, confirm)   | §2.2 Step 3                                         |
| FR-062 (registration, Summary legibility)     | §2.2 Step 6.5                                       |
| FR-070 (GTM skill + output)                   | §3.2 Step 4                                         |
| FR-071 (launch-type distinction)              | §3.2 Step 3                                         |
| FR-072 (brief.md by-product)                  | §3.2 Step 6.5                                       |
| NFR-010/011 (degradation, ask-once)           | §2.2 Step 2, §3.2 Step 2                            |
| NFR-021 (no duplicated framework content)     | §1 — both skills reference `campaign-frameworks.md` |
| NFR-030/031 (delimited output, step sequence) | Both skills' Step sequences                         |
| OQ-007 (gated needs, this slice's two skills) | §2.2 Step 2, §3.2 Step 2                            |

---
