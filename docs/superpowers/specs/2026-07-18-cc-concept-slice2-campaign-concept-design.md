# cc-concept — Slice 2 Design: Campaign Concept Skill

**Status:** Approved for implementation
**Date:** 2026-07-18
**Source briefing:** `requirements-cc-concept.md` (v2.1)
**Scope:** Slice 2 of 5 (campaign-concept skill + brief.md handoff)

---

## 1. Purpose and scope

Slice 1 delivered the foundation: the shared skill contract, the positioning
framework library, and two working skills (`cc-concept-onboarding`,
`cc-concept-positioning`). Slice 2 adds the third skill named in the five-slice
decomposition: **`cc-concept-campaign-concept`**, which turns a campaign
objective into a complete campaign concept — goals, audience, key messages,
channel mix, and creative brief — and hands the result to `cc-content` as
`brief.md`.

This is the slice that closes the loop the whole plugin exists to build: a
strategy output that `cc-content` skills can consume directly, satisfying
BG-03 and the campaign-brief success criterion in the requirements' §2.3.

**In scope:** the campaign-concept skill, its framework library, and the
brief.md handoff mechanics (FR-030–FR-033, CON-003).

**Out of scope:** everything in Slices 3–5 (advisor skills, planning skills,
learnings-promotion skill). No changes to `cc-concept-onboarding` or
`cc-concept-positioning` — both already collect what this skill needs.

Two new files only:

```
plugins/cc-concept/skills/cc-concept-campaign-concept/SKILL.md
plugins/cc-concept/skills/_shared/campaign-frameworks.md
```

---

## 2. The skill — `cc-concept-campaign-concept`

### 2.1 Frontmatter

`name: cc-concept-campaign-concept`. Trigger phrases: "plan a campaign",
"campaign concept", "build a campaign brief", and similar. `argument-hint:
"[--type product-launch|thought-leadership|seasonal-promotion|retention|lead-generation|brand-awareness]"`.

### 2.2 Step sequence

The skill references `_shared/skill-contract.md` for its run sequence rather
than restating it (Steps 0, 1, 5, 6, 7). Skill-specific behavior:

**Step 0–1 (contract).** Recall learnings; load context. Looks for: business
goals/KPIs and target audience (preferring a `cc-concept-positioning` output
file if one is registered, else organization background) as the two gated
needs. Noted silently if present, never asked about: competitive landscape,
current marketing channels, growth stage, and any brand-specific strategy
overrides (FR-006).

**Step 2 — Gating check (this slice's resolution of OQ-007).** Three-state
model, evaluated independently per need, matching the pattern Slice 1
established for positioning: _covered_ / _absent-but-supplied_ (ask once) /
_absent-and-unanswered_ (⚠ DEGRADED, output still generates) — for **business
goals** and **target audience**. These are the two needs this skill treats as
required; everything else is optional and never gates.

**Step 3 — Calibrate.** If `--type` was passed, use it directly and skip the
campaign-type question (FR-033). Otherwise infer campaign type, funnel stage,
and B2B/B2C from loaded context (FR-032); where inference isn't confident, ask
the missing question directly rather than guessing. Present a one-line
inference summary (e.g. "Type: product launch · Audience: B2B mid-market ·
Stage: TOFU") and wait for user confirmation or correction before drafting.

**Step 4 — Generate.** Apply the three frameworks from
`_shared/campaign-frameworks.md` compositionally (see §3): SOSTAC shapes the
whole output, RACE structures the channel-mix section, Message House
structures the key-messages section. Produce: campaign name, objective,
target audience summary, at least two key messages, proposed channel mix, and
a creative brief section (tone/voice notes if brand-voice context is loaded,
primary CTA, constraints, suggested formats per channel).

**Step 5–6 (contract).** Internal quality check — verify all of FR-030's
required elements are present — then delimited output, prefixed with `⚠
DEGRADED OUTPUT — generated without: <needs>` if Step 2 landed in the
degraded state.

**Step 6.5 — Offer to save as `brief.md`.** See §4.

**Step 7 (contract).** Two-phase feedback, tagged
`[cc-concept:cc-concept-campaign-concept]`.

---

## 3. Framework library — `_shared/campaign-frameworks.md`

Structured like `positioning-frameworks.md` (frameworks + selection process +
project-override), but the three frameworks are **composable by facet**, not
alternatives to pick between — they answer different questions and are all
applied on every run:

- **SOSTAC** (Situation, Objectives, Strategy, Tactics, Action, Control) —
  shapes the whole output. Mapping: Situation/Objectives → campaign
  name+objective+audience; Strategy/Tactics → key messages; Action → channel
  mix; Control → the creative brief's success framing.
- **RACE** (Reach, Act, Convert, Engage) — applied specifically inside the
  channel-mix section, sequencing channels by funnel stage. Includes guidance
  on stage emphasis by campaign type (product-launch weights Reach+Act;
  retention weights Engage) — this informs but does not override the
  funnel-stage inference from Step 3.
- **Message House** (roof statement, pillars, proof points) — applied
  specifically inside the key-messages section.

**Selection process:** documents the three-way mapping above (which
framework governs which output section) rather than a decision tree, since
these frameworks are not mutually exclusive choices.

**Project-override rule (FR-082):** if loaded context expresses a framework
preference or prohibition (e.g. "never sequence channels with RACE, always
use our own funnel model"), the skill honors it and states so — same
mechanism as positioning's project-override rule.

---

## 4. brief.md handoff

### 4.1 Compatibility contract (CON-003)

No formal schema — `cc-content` skills read a briefing by comprehension, not
by parsing (per the requirements' ASS-002/OQ-002 resolution). Before offering
to save, Step 5's internal quality check confirms the four elements
`cc-content` skills extract are present in prose: campaign objective → goals,
key messages → key messages, creative brief's constraints → constraints,
creative brief's CTA → CTAs.

### 4.2 Location

Fixed at `brief.md` in the working-directory root — never under `context/` —
matching exactly where `cc-content`'s zero-argument discovery (`ls brief.md`)
looks.

### 4.3 Collision handling (NFR-040)

If `brief.md` already exists, the skill never overwrites it silently. It
shows a one-line summary (campaign name + last-modified, read from the
existing file) and asks: overwrite / save under a different name / cancel.

### 4.4 Not a context file

Per the requirements' Glossary, a campaign brief is a distinct concept from a
context file — a transient handoff artifact, not enduring brand context.
`brief.md` is **not** registered in the `## Context files` table.
`cc-content` discovers it positionally (`$ARGUMENTS`, else `ls brief.md`),
not via the context mechanism.

---

## 5. This slice's resolution of OQ-006

`cc-concept-campaign-concept` produces a full campaign document (goals,
audience, messages, channel mix, creative brief) — a structurally different
artifact from `cc-content-ideation`'s content angles or `cc-content-text`'s
single-piece drafting. No overlap by construction; no deferral logic is
needed between these skills. OQ-006 remains open for the marketing-advisor
skill in Slice 3, where FR-042's deferral behavior actually applies.

---

## 6. File layout and config updates

New files (see §1). `CLAUDE.md`'s Key Config Files table gets a new row for
the SKILL.md, with its description pre-populated at creation time — avoiding
the placeholder-TODO churn Slice 1's registration produced.

---

## 7. Verification

Fixtures to run manually post-implementation (same discipline as Slice 1's
§5 — written here, executed later):

**Fixture A — bare project.** No `cc-content`, no prior `cc-concept`
onboarding or positioning. Invoking the skill hits the degraded path for both
gated needs (business goals, target audience); confirms the pause/degrade
choice is offered once per need and the output carries the `⚠ DEGRADED
OUTPUT` prefix when the user continues. Proves NFR-041 (standalone) and
NFR-010/011 (degradation mechanics).

**Fixture B — onboarded + positioned project.** `cc-concept-onboarding` and
`cc-concept-positioning` have both run. Invoking the skill finds both gated
needs covered from the positioning output and onboarding context, with no
questions asked for them. Proves the context-reuse path and the
positioning-output preference stated in §2.2.

**Fixture C — campaign-type argument.** Invoking the skill with `--type
retention` skips the campaign-type inference question and applies RACE's
retention-weighted (Engage-heavy) guidance. Proves FR-033.

**Fixture D — brief.md collision.** A `brief.md` already exists in the
working directory. Invoking the skill shows the existing file's summary and
honors overwrite / save-as / cancel. Proves §4.3 / NFR-040.

---

## 8. Traceability to the briefing

| Requirement                                   | Where addressed                                                                          |
| --------------------------------------------- | ---------------------------------------------------------------------------------------- |
| FR-030 (skill + required output elements)     | §2.2 Steps 3–4                                                                           |
| FR-031 (brief.md handoff)                     | §2.2 Step 6.5, §4                                                                        |
| FR-032 (inference + confirmation)             | §2.2 Step 3                                                                              |
| FR-033 (campaign-type argument)               | §2.2 Step 3, §2.1 frontmatter                                                            |
| CON-003 (element coverage, discoverability)   | §4.1, §4.2                                                                               |
| NFR-030/031 (delimited output, step sequence) | §2.2, shared-contract reference                                                          |
| NFR-040 (no conflicting writes)               | §4.3                                                                                     |
| NFR-041 (standalone)                          | Satisfied by construction — no dependency on `cc-content`, same precedent as positioning |
| This slice's OQ-007 (gating)                  | §2.2 Step 2                                                                              |
| OQ-006 (delineation, partial)                 | §5                                                                                       |

---
