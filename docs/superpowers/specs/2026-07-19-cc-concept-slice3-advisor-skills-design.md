# cc-concept — Slice 3 Design: Advisor Skills

**Status:** Approved for implementation
**Date:** 2026-07-19
**Source briefing:** `requirements-cc-concept.md` (v2.1)
**Scope:** Slice 3 of 5 (marketing advisor + channel advisor)

---

## 1. Purpose and scope

Slice 3 adds the two "advisor" skills named in the five-slice decomposition
(Slice 1 design §1.1): **`cc-concept-marketing-advisor`** (open-ended
strategic Q&A, FR-040–042) and **`cc-concept-channel-advisor`** (structured
channel-mix recommendation, FR-050–052). Together they close the gap between
the templated skills Slices 1–2 delivered (positioning, campaign-concept) and
unstructured strategy questions that don't fit a fixed template.

**In scope:** the two skill files, both referencing the existing
`_shared/skill-contract.md` and channel-advisor reusing the RACE model from
`_shared/campaign-frameworks.md`. No new shared framework file — RACE
already fits FR-050–052's shape, and FR-083 favors starting small over
authoring a framework ahead of proven need.

**Out of scope:** Slice 4 (content-strategy, GTM) and Slice 5
(learnings-promotion). No changes to `cc-concept-onboarding`,
`cc-concept-positioning`, or `cc-concept-campaign-concept`.

Two new files only:

```
plugins/cc-concept/skills/cc-concept-marketing-advisor/SKILL.md
plugins/cc-concept/skills/cc-concept-channel-advisor/SKILL.md
```

---

## 2. The skill — `cc-concept-marketing-advisor`

### 2.1 Frontmatter

`name: cc-concept-marketing-advisor`. Trigger phrases: "help me think
through...", "marketing advice on...", or any open-ended strategic question
that doesn't match a templated skill's trigger. No `argument-hint` beyond
the free-text question — `$ARGUMENTS` is the question itself.

### 2.2 Step sequence

References `_shared/skill-contract.md` for its run sequence. The contract's
linear steps map onto a conversational loop rather than one
generate-and-done pass — the skill re-enters Steps 3–7 on each substantive
question within the same invocation, not just once.

**Step 0–1 (contract).** Recall learnings; load the `## Context files` table
by Summary. No fixed need list — the relevant context varies per question.

**Step 2 — Gating (this slice's resolution of OQ-007 for this skill): none.**
The advisor gates on nothing. It uses whatever context is loaded and, when a
specific answer would clearly benefit from an uncovered need, notes the gap
inline in that answer (e.g. "I don't have your business goals on file, so
this leans generic") rather than the ask-once/⚠ DEGRADED ceremony the
templated skills use. NFR-010 is satisfied vacuously: there is no required
need for output to be degraded without.

**Step 3 — Deferral check (this slice's resolution of OQ-006 and FR-042).**
Before answering, check whether the question falls squarely within a more
specific skill's scope:

- `cc-concept-channel-advisor` — channel mix or tactics questions
- `cc-concept-positioning` — differentiation or value-proposition questions
- `cc-concept-campaign-concept` — full campaign planning questions
- `cc-content-ideation` — content angle/inspiration questions (cross-plugin)
- `cc-content-text` — drafting a specific piece of content (cross-plugin)

The two `cc-content-*` deferrals apply **only if those skills are available
in the current session's toolset** (i.e. `cc-content` is installed) — never
assumed, matching NFR-041's standalone requirement: `cc-content`'s presence
enhances this behavior, its absence never breaks anything. If a match is
found, name the specific skill and suggest invoking it instead of answering
inline. The user may say "answer anyway" to proceed with an inline answer
regardless.

**Step 4 — Generate.** Produce a conversational, strategically-grounded
answer sized to the question — no fixed section skeleton (this slice's
resolution of OQ-005). Reference loaded context by name when it informed
the answer.

**Step 5–6 (contract).** Internal quality check, then delimited output per
NFR-030 — every reply is wrapped in the `─────` delimiter block with a
topic header (e.g. `## Positioning vs. Messaging`), even though the content
inside is free-form prose rather than a template.

**Step 7 — Save-prompt (FR-041, this slice's resolution of prompt timing).**
After each reply that surfaces a decision, direction, or constraint worth
keeping, offer to persist it:

- as a `.claude/learnings.md` entry (lightweight, default), or
- as a **new**, collision-checked context file, registered in the
  `## Context files` table.

The advisor never edits an existing context file it did not create — only
ever writes a new file, collision-checked the same way positioning does.
This replaces the shared contract's generic Step 7 with a per-turn version
specific to this skill's multi-turn nature: the offer fires after each
qualifying reply, not once at a session boundary that an open-ended chat may
never explicitly reach.

---

## 3. The skill — `cc-concept-channel-advisor`

### 3.1 Frontmatter

`name: cc-concept-channel-advisor`. Trigger phrases: "recommend a channel
mix", "which channels should we use", "channel strategy for...".
`argument-hint: "[optional: goal or campaign this recommendation is for]"`.

### 3.2 Step sequence

References `_shared/skill-contract.md` for its run sequence. One-shot
generate-and-done, the same shape as `cc-concept-positioning` and
`cc-concept-campaign-concept`.

**Step 0–1 (contract).** Recall learnings; load the `## Context files` table
by Summary. Looks for: **business goals** and **target audience** (the two
gated needs), plus current marketing channels and budget — noted silently if
present, never asked about (FR-051, FR-052).

**Step 2 — Gating (this slice's resolution of OQ-007 for this skill).**
Three-state model, evaluated independently, on **business goals** and
**target audience** — the same pattern Slice 2 established for
campaign-concept. Current channels and budget stay silent-only: FR-052's
"flag when a channel may be out of reach" only fires when that context
happens to be loaded; it never blocks the recommendation.

**Step 3 — Calibrate.** Take the goal from `$ARGUMENTS` if given, else from
loaded business goals or the Step 2 gating answer. No campaign-type
inference is needed here — that is campaign-concept's job — just goal,
audience, and whatever current-channel/budget context is loaded.

**Step 4 — Generate.** Apply RACE from `../_shared/campaign-frameworks.md`.
**State the choice before generating:**

> "Using RACE to sequence channels by funnel stage."

Produce:

- Recommended primary channel(s) with rationale (FR-050).
- Recommended supporting channel(s).
- At least one tactical recommendation per recommended channel.
- For each recommended channel, a maintain/grow/reduce/exit call **if**
  current channels were loaded (FR-051).
- A "prerequisites" note for any recommended channel where the loaded
  context suggests it may be out of reach — budget, capability, or skills
  the user may not have (FR-052).

**Step 5–6 (contract).** Internal quality check verifies all of FR-050's
required elements are present, then delimited output per NFR-030, prefixed
with `⚠ DEGRADED OUTPUT — generated without: <needs>` if Step 2 landed in
the degraded state (matching the fix applied to campaign-concept in Slice 2).

**Step 7 (contract).** Two-phase feedback, tagged
`[cc-concept:cc-concept-channel-advisor]`.

---

## 4. File layout and config updates

Two new SKILL.md files (§1). No new `_shared/` file:
`cc-concept-channel-advisor/SKILL.md` references
`../_shared/campaign-frameworks.md` directly — a small cross-reference from
one skill's directory to another's shared file, the same pattern
`cc-concept-campaign-concept` already uses for its own frameworks file.

`CLAUDE.md`'s Key Config Files table gets two new rows, with descriptions
pre-populated at creation time — avoiding the sync-hook TODO-placeholder
churn Slices 1–2 both had to correct after the fact.

---

## 5. Verification

Fixtures to run manually post-implementation (same discipline as Slices
1–2's — written here, executed later):

**Fixture A — deferral.** Ask the marketing advisor a channel-mix-shaped
question (e.g. "what channels should we focus on?"). Expected: it names
`cc-concept-channel-advisor` and suggests invoking it instead of answering
inline, without refusing outright if the user insists on an inline answer.
Proves FR-042 and this slice's resolution of OQ-006.

**Fixture B — advisor save-prompt.** Ask the marketing advisor an open
strategic question that surfaces a clear decision. Expected: the reply is
delimited and headed per NFR-030, and ends with an offer to save the
decision (learnings vs. a new context file) — not a generic "let me know if
you want anything else." Proves FR-041.

**Fixture C — channel advisor, bare project.** No context. Expected: both
gated needs (business goals, target audience) hit the ask-once/degrade path;
current channels and budget are never asked about. Proves NFR-041, NFR-011,
and this slice's resolution of OQ-007 for this skill.

**Fixture D — channel advisor, current channels loaded.** A project with a
context file describing existing channels. Expected: the recommendation
explicitly calls out maintain/grow/reduce/exit for each existing channel.
Proves FR-051.

---

## 6. Traceability to the briefing

| Requirement                                   | Where addressed                                                   |
| --------------------------------------------- | ----------------------------------------------------------------- |
| FR-040 (marketing advisor skill)              | §2.2 Steps 3–4                                                    |
| FR-041 (session save-prompt)                  | §2.2 Step 7                                                       |
| FR-042 (deferral to specific skills)          | §2.2 Step 3                                                       |
| FR-050 (channel advisor skill + output)       | §3.2 Steps 3–4                                                    |
| FR-051 (uses goals + current channels)        | §3.2 Steps 0–1, 4                                                 |
| FR-052 (prerequisites flagging)               | §3.2 Step 4                                                       |
| NFR-010/011 (degradation, ask-once)           | §2.2 Step 2 (vacuous), §3.2 Step 2                                |
| NFR-030/031 (delimited output, step sequence) | Both skills' Step sequences                                       |
| NFR-041 (standalone)                          | §2.2 Step 3 (cross-plugin deferral is conditional, never assumed) |
| OQ-005 (advisor output structure)             | §2.2 Step 4 — resolved: conversational, still delimited           |
| OQ-006 (delineation vs. cc-content, extended) | §2.2 Step 3 — resolved: deferral list includes cc-content skills  |
| OQ-007 (gated needs, this slice's two skills) | §2.2 Step 2, §3.2 Step 2                                          |

---
