# cc-concept — Slice 5 Design: Learnings Promotion Skill

**Status:** Approved for implementation
**Date:** 2026-07-19
**Source briefing:** `requirements-cc-concept.md` (v2.1)
**Scope:** Slice 5 of 5 (learnings-promotion skill)

---

## 1. Purpose and scope

Slice 5 adds the final skill named in the five-slice decomposition
(Slice 1 design §1.1): **`cc-concept-learnings-promotion`** (FR-080,
FR-080a). It detects recurring `[cc-concept:`-tagged patterns in
`.claude/learnings.md` and offers to promote them into a durable location,
or dismisses them as one-offs — closing the feedback loop every other
skill's Step 7 opens but never resolves on its own.

**Precedent followed:** `cc-config-optimize`'s "Learnings review" step
(`plugins/cc-config/skills/cc-config-optimize/SKILL.md` §2g), which FR-080's
rationale explicitly cites as the model. That skill's mechanics translate
directly: group similar entries, flag groups of 3+ as a real recurring
pattern, propose a promotion target per group, wait for approval, then apply
and remove processed entries from `learnings.md` — deleting the file
entirely if nothing remains.

**In scope:** one new skill file. No new `_shared/` file — this is a
maintenance skill, not a strategy-generation skill, and needs no framework
library.

**Out of scope:** nothing else remains after this slice — Slices 1–4
already delivered the full plugin surface named in the decomposition.

One new file only:

```
plugins/cc-concept/skills/cc-concept-learnings-promotion/SKILL.md
```

---

## 2. The skill — `cc-concept-learnings-promotion`

### 2.1 Frontmatter

`name: cc-concept-learnings-promotion`. Trigger phrases: "promote
learnings", "review cc-concept learnings", "consolidate learnings",
"clean up learnings.md" — deliberately excluding `cc-content-session-wrap`'s
four trigger phrases ("wrap up", "end session", "session wrap", "close out
this session") per FR-080a. No `argument-hint`.

### 2.2 Design decisions

- **Scope filter (FR-080).** Reads `.claude/learnings.md` but considers
  only lines tagged `[cc-concept:` — every other plugin's tags are invisible
  to this skill for promotion purposes, satisfying FR-080's "reads no other
  plugin's tags."
- **Promotion targets — two, matching FR-080's wording, disambiguated by the
  cc-config-optimize precedent:**
  1. **The project's CLAUDE.md** — the common case (client/project-specific
     preferences, e.g. "prefers email+LinkedIn as primary channels").
     Written as prose guidance under a project-owned section of CLAUDE.md,
     never into the `## Context files` or `## Key Config Files` tables.
  2. **A cc-concept-owned reference file** (a `_shared/*.md` file or a
     `SKILL.md`) — reserved for the rare case where a pattern reflects a
     genuinely universal, project-independent insight about how a
     framework or skill should behave, not a client preference. The skill
     must explicitly justify why a candidate is universal before offering
     this target, since every existing `_shared/*.md` file already states
     that project-specific preferences don't belong there (see
     `positioning-frameworks.md`'s and `campaign-frameworks.md`'s override
     rules).
- **One-off entries** (fewer than 3 similar entries): proposed for
  dismissal (deletion from `learnings.md`), not promotion.
- **No gating, no context-table dependency.** This skill operates entirely
  on `.claude/learnings.md`, not on project context — this slice's
  resolution of OQ-007 for this skill is that gating doesn't apply.
- **FR-080a hard constraints:** no session review, no deliverable
  promotion, **no git commits** — the skill writes files but never runs
  `git add`/`git commit`; that stays with the user's own workflow. Trigger
  phrases explicitly exclude `cc-content-session-wrap`'s four phrases.
- **After applying:** processed entries (both promoted and dismissed) are
  removed from `.claude/learnings.md`; the file is deleted entirely if
  nothing remains — matching `cc-config-optimize`'s exact behavior.

### 2.3 Step sequence

This skill adapts the shared contract (`_shared/skill-contract.md`) rather
than following it literally — its whole job is what the contract's Step 0
normally does silently in the background.

**Step 0 — Read and filter.** Read `.claude/learnings.md`. If absent,
report nothing to promote and stop — this is not an error state. Filter to
`[cc-concept:`-tagged lines only; ignore every other plugin's tags entirely.

**Step 1 — Group and threshold.** Group the filtered entries by semantic
similarity (the skill's own judgment — no fixed taxonomy). Flag any group
of **3 or more** similar entries as a recurring pattern (FR-080's fit
criterion). Groups with fewer than 3 are one-off candidates for dismissal.

**Step 2 — Propose targets.** For each recurring group, propose one
promotion target — CLAUDE.md by default, or a specific `_shared/*.md`/
`SKILL.md` file only if the pattern is genuinely universal — with a
one-line rationale for each proposal.

**Step 3 — Delimited output.** Present the full grouped list inside the
NFR-030 delimiter block: promote-candidates (each with proposed target +
rationale) and one-offs (marked for dismissal). Wait for the user's
per-group promote/dismiss/skip decision. Never apply anything before
approval.

**Step 4 — Apply.** Write approved promotions to their chosen targets.
Remove all processed entries (both promoted and dismissed) from
`.claude/learnings.md`. Delete the file entirely if nothing remains. Perform
no git operations of any kind.

---

## 3. File layout and config updates

One new SKILL.md file (§1). `CLAUDE.md`'s Key Config Files table gets one
new row, with its description pre-populated at creation time — the Task 3
pattern established in Slices 2–4.

---

## 4. Verification

Fixtures to run manually post-implementation (same discipline as prior
slices — written here, executed later):

**Fixture A — recurring pattern detected.** Seed `.claude/learnings.md`
with 3+ semantically similar `[cc-concept:`-tagged entries (e.g. three
entries about a client preferring a specific channel mix) plus one unrelated
`[cc-concept:`-tagged one-off, plus at least one `[cc-content:`-tagged entry.
Invoke `/cc-concept-learnings-promotion` (or an equivalent trigger phrase).
Expected: the recurring group is proposed for promotion with a rationale,
the one-off is proposed for dismissal, and the `[cc-content:` entry is never
mentioned. Proves FR-080's fit criterion and the plugin-tag scope filter.

**Fixture B — trigger phrase non-collision.** In a project with both
`cc-concept` and `cc-content` installed, say "wrap up".
Expected: `cc-content-session-wrap` is invoked, not
`cc-concept-learnings-promotion`. Proves FR-080a.

**Fixture C — apply and cleanup.** Approve one promotion to CLAUDE.md and
one dismissal from Fixture A's setup.
Expected: the approved pattern appears as prose in CLAUDE.md (not in the
Context files or Key Config Files tables); both the promoted and dismissed
entries are removed from `.claude/learnings.md`; no `git add`/`git commit`
was run. Proves the Step 4 apply/cleanup mechanics and the no-git-commits
constraint.

**Fixture D — empty learnings file.** Run `/cc-concept-learnings-promotion`
in a project with no `.claude/learnings.md`.
Expected: the skill reports nothing to promote and stops cleanly — no
error, no fabricated groups.

---

## 5. Traceability to the briefing

| Requirement                                                | Where addressed                    |
| ---------------------------------------------------------- | ---------------------------------- |
| FR-080 (detection, grouping, promotion)                    | §2.2, §2.3 Steps 0–3               |
| FR-080a (no session review/commits, trigger non-collision) | §2.2, §2.1                         |
| OQ-007 (gated needs, this slice's skill)                   | §2.2 — resolved: no gating applies |

---
