---
name: cc-concept-learnings-promotion
description: >
  Use this skill to review accumulated cc-concept learnings in .claude/learnings.md,
  group recurring patterns, and promote them into durable guidance (CLAUDE.md or a
  cc-concept reference file) or dismiss one-offs. Invoke when the user asks to
  "promote learnings", "review cc-concept learnings", "consolidate learnings", or
  "clean up learnings.md". Never triggers on session-wrap phrasing ("wrap up", "end
  session", "session wrap", "close out this session") — that is cc-content-session-wrap's
  scope, not this skill's.
allowed-tools: Read, Write, Edit
---

# Learnings Promotion Skill

This skill closes the feedback loop every other cc-concept skill's Step 7 opens but never resolves on its own — it reviews `.claude/learnings.md`, groups recurring `[cc-concept:`-tagged patterns, and promotes or dismisses them.

This skill does not follow ../_shared/skill-contract.md's step sequence literally — its whole job is what the contract's Step 0 normally does silently in the background. No gating applies: this skill operates entirely on .claude/learnings.md, not on project context.

## Step 0: Read and filter

Read `.claude/learnings.md`. If the file does not exist, report "No learnings file found — nothing to promote" and stop. This is not an error state.

Filter to lines tagged `[cc-concept:` only — ignore every other plugin's tags entirely (e.g. `[cc-content:`, `[cc-config:` lines are invisible to this skill). Example of a matching line:

```
[cc-concept:cc-concept-channel-advisor] client prefers email+LinkedIn as primary channels over paid social — 2026-06-01
```

## Step 1: Group and threshold

Group the filtered entries by semantic similarity — this skill's own judgment, no fixed taxonomy. Flag any group of 3 or more similar entries as a recurring pattern. Groups with fewer than 3 entries are one-off candidates for dismissal.

Example:

```
Three entries about a client's channel preference → recurring pattern, propose promotion.
One unrelated entry about a one-time positioning framework choice → one-off, propose dismissal.
```

## Step 2: Propose targets

For each recurring group, propose exactly one promotion target with a one-line rationale:

- **CLAUDE.md (default, common case).** Client/project-specific preferences — e.g. a channel mix preference, a recurring framework choice, a tone or cadence preference. Written as prose guidance under a project-owned section of CLAUDE.md — never into the `## Context files` or `## Key Config Files` tables.
- **A cc-concept-owned reference file (`_shared/*.md` or a `SKILL.md`) — rare.** Reserved only for a pattern that reflects a genuinely universal, project-independent insight about how a framework or skill should behave — not a client preference. Before offering this target, explicitly state why the candidate is universal rather than project-specific: every existing `_shared/*.md` file already states that project-specific preferences don't belong there, so the default assumption is CLAUDE.md, and this target requires an explicit override justification, not just a hunch.

State each proposal as: group summary, entry count, proposed target, one-line rationale. For groups with fewer than 3 entries: State each as a one-off proposed for dismissal, with a one-line reason (e.g. "single occurrence, no supporting pattern").

## Step 3: Delimited output

Present the full grouped list inside clear delimiters:

```
─────────────────────────────────────────────────────────────────
## Learnings Review
─────────────────────────────────────────────────────────────────

[Grouped list: recurring patterns with proposed targets + rationale,
one-offs marked for dismissal]

─────────────────────────────────────────────────────────────────
```

Wait for the user's per-group decision — promote / dismiss / skip — for each proposed group. Never apply anything before approval. "Skip" leaves the entry in .claude/learnings.md untouched for a future run.

## Step 4: Apply

For each group the user approved for promotion: write the guidance to the approved target. If the target is CLAUDE.md, append as prose under a clearly labeled section (do not touch the `## Context files` or `## Key Config Files` tables). If the target is a `_shared/*.md` or `SKILL.md` file, add the guidance in a location consistent with that file's existing structure.

Remove all processed entries — both promoted and dismissed — from .claude/learnings.md. Entries the user chose to skip remain untouched. If no entries remain after removal, delete .claude/learnings.md entirely.

Perform no git operations of any kind — no git add, no git commit, no git anything. Writing and removing files is this skill's full scope; committing stays with the user's own workflow (FR-080a).

## Scope boundary

This skill never reviews session content, never promotes deliverables (campaign concepts, positioning docs, etc. — those are registered as context by their own skills' Step 6.5), and never triggers on cc-content-session-wrap's phrasing ("wrap up", "end session", "session wrap", "close out this session"). Its only input is `.claude/learnings.md`, filtered to `[cc-concept:` tags.
