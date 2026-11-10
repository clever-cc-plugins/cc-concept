---
name: learnings-promotion
description: >
  Use this skill to review accumulated cc-concept learnings in
  .claude/learnings.md, group related entries, and promote them into durable
  guidance (CLAUDE.md, a registered context file or a cc-concept reference file),
  keep them or retire them. Invoke when the user asks to "promote learnings",
  "review cc-concept learnings", "consolidate learnings", or "clean up
  learnings.md". Never triggers on session-wrap phrasing ("wrap up", "end
  session", "session wrap", "close out this session") — that is session-wrap's
  scope, not this skill's.
allowed-tools: Read, Write, Edit
---

# Learnings Promotion Skill

This skill closes the feedback loop every other cc-concept skill's Step 7 opens but never resolves on its own — it reviews `.claude/learnings.md`, groups related `[cc-concept:`-tagged entries, and promotes, keeps or retires them.

This skill does not follow ../_shared/skill-contract.md's step sequence literally — its whole job is what the contract's Step 0 normally does silently in the background. No gating applies: this skill operates entirely on .claude/learnings.md, not on project context.

## Step 0: Read and filter

Read `.claude/learnings.md`. If the file does not exist, report "No learnings file found — nothing to promote" and stop. This is not an error state.

Filter to lines tagged `[cc-concept:` only — ignore every other plugin's tags entirely (e.g. `[cc-content:`, `[cc-config:` lines are invisible to this skill). Example of a matching line:

```
[cc-concept:channel-advisor] client prefers email+LinkedIn as primary channels over paid social (stated) — 2026-06-01
```

Read `../_shared/learnings-protocol.md` and follow its **Reviewing** section. Also read `CLAUDE.md` and the registered context files, so you can tell which entries are already covered.

## Step 1: Group and propose

Group the filtered entries by the concern they express, however they are worded — this skill's own judgment, no fixed taxonomy. There is no minimum group size: a single `stated`, `corrected` or unmarked entry can be a promotion candidate. For an unmarked entry, judge from its wording whether the user said it, and say so in the proposal. Frequency is a signal, not a threshold. Context files are the ones registered in the `## Context files` table in `CLAUDE.md`; match them to an entry by their Summary column.

Example:

```
Three entries about a client's channel preference → promote together.
One stated entry about a client's tone preference → promote on its own.
One inferred entry about a one-time framework choice → keep.
```

## Step 2: Propose targets

For each proposal, name the action (promote, keep or retire) and, for a promotion, exactly one target with a one-line rationale:

- **CLAUDE.md (default when no context file holds the subject).** Client/project-specific preferences — e.g. a channel mix preference, a recurring framework choice, a tone or cadence preference. Written as prose guidance under a project-owned section of CLAUDE.md — never into the `## Context files` or `## Key Config Files` tables.
- **A registered context file — takes precedence over CLAUDE.md.** When the entry is about the client (audience, market, brand facts) rather than about how a skill should behave and a registered context file already holds that subject, use that file; otherwise CLAUDE.md is the default.
- **A cc-concept-owned reference file (`_shared/*.md` or a `SKILL.md`) — rare.** Reserved only for a pattern that reflects a genuinely universal, project-independent insight about how a framework or skill should behave — not a client preference. Before offering this target, explicitly state why the candidate is universal rather than project-specific: every existing `_shared/*.md` file already states that project-specific preferences don't belong there, so the default assumption is CLAUDE.md, and this target requires an explicit override justification, not just a hunch.

State each proposal as: group summary, entry count, sources, proposed action and target, one-line rationale. Propose **keep** for an entry that is still true but not yet a standing rule, and **retire** for one already covered (name the file), contradicted, superseded or tied to a situation that is over.

## Step 3: Delimited output

Present the full list of proposals inside clear delimiters:

```
─────────────────────────────────────────────────────────────────
## Learnings Review
─────────────────────────────────────────────────────────────────

[List of proposals: entry count, sources, target (for promotions)
and one-line reason for each]

─────────────────────────────────────────────────────────────────
```

Wait for the user's per-proposal decision — promote / keep / retire. Never apply anything before approval. "Keep" leaves the entry in .claude/learnings.md untouched for a future run.

## Step 4: Apply

For each proposal the user approved for promotion: write the guidance to the approved target. If the target is CLAUDE.md, append as prose under a clearly labeled section (do not touch the `## Context files` or `## Key Config Files` tables). If the target is a registered context file, `_shared/*.md` or `SKILL.md` file, add the guidance in a location consistent with that file's existing structure.

Remove all promoted and retired entries from .claude/learnings.md. Kept entries remain untouched. If no entries remain below the header after removal, delete .claude/learnings.md, or leave only the header if you cannot delete files.

Perform no git operations of any kind — no git add, no git commit, no git anything. Writing and removing files is this skill's full scope; committing stays with the user's own workflow (FR-080a).

## Scope boundary

This skill never reviews session content, never promotes deliverables (campaign concepts, positioning docs, etc. — those are registered as context by their own skills' Step 6.5), and never triggers on session-wrap's phrasing ("wrap up", "end session", "session wrap", "close out this session"). Its only input is `.claude/learnings.md`, filtered to `[cc-concept:` tags.
