# cc-concept Slice 5 (Learnings Promotion) Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add the `cc-concept-learnings-promotion` skill to the existing `cc-concept` plugin — the final skill in the five-slice decomposition — which detects recurring `[cc-concept:`-tagged patterns in `.claude/learnings.md` and offers to promote them to CLAUDE.md or a cc-concept-owned reference file, dismissing one-offs.

**Architecture:** One new Markdown file under the existing `cc-concept` plugin repo (`plugins/cc-concept/skills/`). No new `_shared/` file — this is a maintenance skill, not a strategy-generation skill. No new infra, no new plugin registration. There is no compiled code and no unit-test runner; "tests" are structural assertions (`grep`, `python3` YAML parse) plus a final round of manual fixture runs (spec §4). This is the last slice — no further slices follow.

**Tech Stack:** Markdown (skill file), `prettier` (repo's PostToolUse formatter), `python3` (frontmatter/YAML validity checks), `gitleaks` (pre-commit secret scan).

## Global Constraints

- **Design source of truth:** `docs/superpowers/specs/2026-07-19-cc-concept-slice5-learnings-promotion-design.md`. Every task traces to it.
- **Repo layout standard:** `marketplace/docs/cc-plugin-repo-guideline.md` — do not deviate.
- **Plugin name:** `cc-concept` (already scaffolded). Skill invoked by bare name (`/cc-concept-learnings-promotion`), never namespaced.
- **No secrets** committed. **No `--force`** flags. Fix root causes.
- **Do not copy skill/plugin files between repos.**
- **Scope filter (FR-080):** the skill reads `.claude/learnings.md` but considers only lines tagged `[cc-concept:` — every other plugin's tags are invisible to it.
- **No gating (this slice's OQ-007 resolution):** this skill operates entirely on `.claude/learnings.md`, not on project context — no three-state gating model applies.
- **Grouping threshold (FR-080):** 3 or more semantically similar `[cc-concept:`-tagged entries = a recurring pattern, proposed for promotion. Fewer than 3 = a one-off, proposed for dismissal.
- **Promotion targets:** (1) the project's CLAUDE.md, as prose guidance, never into the `## Context files` or `## Key Config Files` tables — the common case; (2) a cc-concept-owned reference file (`_shared/*.md` or a `SKILL.md`) — reserved for genuinely universal, project-independent insights, and the skill must explicitly justify why a candidate is universal before offering this target.
- **FR-080a hard constraints:** no session review, no deliverable promotion, **no git commits of any kind** — the skill writes files but never runs `git add`/`git commit`. Trigger phrases explicitly exclude `cc-content-session-wrap`'s four trigger phrases ("wrap up", "end session", "session wrap", "close out this session").
- **Apply/cleanup:** after approval, both promoted and dismissed entries are removed from `.claude/learnings.md`; the file is deleted entirely if nothing remains — matching `cc-config-optimize`'s exact behavior (`plugins/cc-config/skills/cc-config-optimize/SKILL.md` §2g).
- **Empty-file handling:** if `.claude/learnings.md` is absent, report nothing to promote and stop — not an error state.

---

## File Structure

| Path                                                                | Responsibility                                                                  |
| ------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| `plugins/cc-concept/skills/cc-concept-learnings-promotion/SKILL.md` | Read/group/propose/apply promotion of recurring `[cc-concept:`-tagged learnings |
| `CLAUDE.md`                                                         | +1 row in the Key Config Files table for the new SKILL.md file                  |

Already present: `docs/superpowers/specs/2026-07-19-cc-concept-slice5-learnings-promotion-design.md`, this plan file, all Slice 1–4 skill files and `_shared/*.md` files (all unmodified).

---

## Task 1: Learnings promotion skill

Deliverable: `cc-concept-learnings-promotion/SKILL.md` — a maintenance skill that reads `.claude/learnings.md`, filters to `[cc-concept:`-tagged lines, groups by similarity, proposes promotion or dismissal, waits for approval, then applies and cleans up (spec §2).

**Files:**

- Create: `plugins/cc-concept/skills/cc-concept-learnings-promotion/SKILL.md`
- Reference (read for shape, do not modify): `plugins/cc-config/skills/cc-config-optimize/SKILL.md` (§2g "Learnings review" — the precedent this skill's mechanics follow)
- Reference (read for shape, do not modify): `plugins/cc-concept/skills/_shared/campaign-frameworks.md` and `_shared/positioning-frameworks.md` (for the exact override-rule wording that says project-specific preferences don't belong in `_shared/*.md` — the justification bar this skill must apply before offering a `_shared/*.md` promotion target)

**Interfaces:**

- Consumes: `.claude/learnings.md` (plain text, one tagged entry per line, format `[<plugin>:<skill>] <observation> — <YYYY-MM-DD>`).
- Produces: prose additions to `CLAUDE.md` (promoted, common case) or a specific `_shared/*.md`/`SKILL.md` file (promoted, rare case); a rewritten or deleted `.claude/learnings.md` (all processed entries removed).

- [ ] **Step 1: Write the SKILL.md frontmatter**

```markdown
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
```

- [ ] **Step 2: Write the skill body**

Body must contain, in order:

1. Intro (H1 `# Learnings Promotion Skill`, then a short paragraph): this skill closes the feedback loop every other cc-concept skill's Step 7 opens but never resolves on its own — it reviews `.claude/learnings.md`, groups recurring `[cc-concept:`-tagged patterns, and promotes or dismisses them.

2. State verbatim: `This skill does not follow ../_shared/skill-contract.md's step sequence literally — its whole job is what the contract's Step 0 normally does silently in the background. No gating applies: this skill operates entirely on .claude/learnings.md, not on project context.`

3. **Step 0** (`## Step 0: Read and filter`): `Read .claude/learnings.md. If the file does not exist, report "No learnings file found — nothing to promote" and stop. This is not an error state.` Then: `Filter to lines tagged [cc-concept: only — ignore every other plugin's tags entirely (e.g. [cc-content:, [cc-config: lines are invisible to this skill).` Include this exact example of a matching line format:

   ```
   [cc-concept:cc-concept-channel-advisor] client prefers email+LinkedIn as primary channels over paid social — 2026-06-01
   ```

4. **Step 1** (`## Step 1: Group and threshold`): `Group the filtered entries by semantic similarity — this skill's own judgment, no fixed taxonomy. Flag any group of 3 or more similar entries as a recurring pattern. Groups with fewer than 3 entries are one-off candidates for dismissal.` Include this exact worked example:

   ```
   Three entries about a client's channel preference → recurring pattern, propose promotion.
   One unrelated entry about a one-time positioning framework choice → one-off, propose dismissal.
   ```

5. **Step 2** (`## Step 2: Propose targets`): `For each recurring group, propose exactly one promotion target with a one-line rationale:`

   ```markdown
   - **CLAUDE.md (default, common case).** Client/project-specific preferences — e.g. a channel mix
     preference, a recurring framework choice, a tone or cadence preference. Written as prose
     guidance under a project-owned section of CLAUDE.md — never into the `## Context files` or
     `## Key Config Files` tables.
   - **A cc-concept-owned reference file (`_shared/*.md` or a `SKILL.md`) — rare.** Reserved only
     for a pattern that reflects a genuinely universal, project-independent insight about how a
     framework or skill should behave — not a client preference. Before offering this target,
     explicitly state why the candidate is universal rather than project-specific: every existing
     `_shared/*.md` file already states that project-specific preferences don't belong there, so
     the default assumption is CLAUDE.md, and this target requires an explicit override
     justification, not just a hunch.
   ```

   Then: `State each proposal as: group summary, entry count, proposed target, one-line rationale.` For groups with fewer than 3 entries: `State each as a one-off proposed for dismissal, with a one-line reason (e.g. "single occurrence, no supporting pattern").`

6. **Step 3** (`## Step 3: Delimited output`): `Present the full grouped list inside clear delimiters:` followed by this fenced block (a single level of triple-backtick fencing, written literally into the SKILL.md body — do not nest it inside another fence):

   ```
   ─────────────────────────────────────────────────────────────────
   ## Learnings Review
   ─────────────────────────────────────────────────────────────────

   [Grouped list: recurring patterns with proposed targets + rationale,
   one-offs marked for dismissal]

   ─────────────────────────────────────────────────────────────────
   ```

   Then: `Wait for the user's per-group decision — promote / dismiss / skip — for each proposed group. Never apply anything before approval. "Skip" leaves the entry in .claude/learnings.md untouched for a future run.`

7. **Step 4** (`## Step 4: Apply`): `For each group the user approved for promotion: write the guidance to the approved target. If the target is CLAUDE.md, append as prose under a clearly labeled section (do not touch the ## Context files or ## Key Config Files tables). If the target is a _shared/*.md or SKILL.md file, add the guidance in a location consistent with that file's existing structure.` Then: `Remove all processed entries — both promoted and dismissed — from .claude/learnings.md. Entries the user chose to skip remain untouched. If no entries remain after removal, delete .claude/learnings.md entirely.` Then state verbatim: `Perform no git operations of any kind — no git add, no git commit, no git anything. Writing and removing files is this skill's full scope; committing stays with the user's own workflow (FR-080a).`

8. Close with a short section (`## Scope boundary`) stating verbatim: `This skill never reviews session content, never promotes deliverables (campaign concepts, positioning docs, etc. — those are registered as context by their own skills' Step 6.5), and never triggers on cc-content-session-wrap's phrasing ("wrap up", "end session", "session wrap", "close out this session"). Its only input is .claude/learnings.md, filtered to [cc-concept: tags.`

- [ ] **Step 3: Verify frontmatter and the filter/threshold/target/no-git markers**

Run:

```bash
f=plugins/cc-concept/skills/cc-concept-learnings-promotion/SKILL.md
python3 - "$f" <<'PY'
import sys, yaml
meta = yaml.safe_load(open(sys.argv[1]).read().split('---')[1])
assert meta['name'] == 'cc-concept-learnings-promotion', meta.get('name')
assert 'allowed-tools' in meta
print("frontmatter OK")
PY
grep -q -i 'wrap up' "$f" && grep -q -i 'end session' "$f" && grep -q -i 'session wrap' "$f" && grep -q -i 'close out this session' "$f" && echo "exclusion phrases OK"
grep -q -- '\[cc-concept:' "$f" && echo "scope filter OK"
grep -q -i '3 or more' "$f" && grep -q -i 'fewer than 3' "$f" && echo "threshold OK"
grep -q -i 'CLAUDE.md' "$f" && grep -q -i '_shared' "$f" && grep -q -i 'universal' "$f" && echo "targets OK"
grep -q -i 'no git operations' "$f" && grep -q -i 'no git add' "$f" && echo "no-git constraint OK"
grep -q -i 'delete .claude/learnings.md entirely' "$f" && echo "cleanup OK"
grep -q -i 'does not exist' "$f" && grep -q -i 'not an error state' "$f" && echo "empty-file handling OK"
grep -q -i 'never into the' "$f" && grep -q -i 'Context files' "$f" && grep -q -i 'Key Config Files' "$f" && echo "table-isolation OK"
```

Expected: `frontmatter OK`, `exclusion phrases OK`, `scope filter OK`, `threshold OK`, `targets OK`, `no-git constraint OK`, `cleanup OK`, `empty-file handling OK`, `table-isolation OK`.

- [ ] **Step 4: Commit**

```bash
git add plugins/cc-concept/skills/cc-concept-learnings-promotion/SKILL.md
git commit -m ":sparkles: feat(cc-concept): add learnings promotion skill"
```

---

## Task 2: CLAUDE.md registration & fixture verification

Deliverable: the new SKILL.md file is registered in `CLAUDE.md`'s Key Config Files table with a real description (no TODO placeholder), and the four verification scenarios from spec §4 pass with the skill invoked for real. This is the final task of the final slice — no further plan follows.

**Files:**

- Modify: `CLAUDE.md` (table row added by the pre-commit sync hook; pre-populate the description before committing so the hook preserves it instead of writing a TODO)
- Reference: spec §4

**Interfaces:**

- Consumes: the file committed in Task 1.

- [ ] **Step 1: Pre-populate the CLAUDE.md row before the sync hook runs**

Open `CLAUDE.md`, find the `## Key Config Files` table, and add this row (matching the table's existing column alignment — `prettier` will realign it):

```markdown
| `plugins/cc-concept/skills/cc-concept-learnings-promotion/SKILL.md` | Skill: Review .claude/learnings.md, promote recurring cc-concept patterns or dismiss one-offs |
```

- [ ] **Step 2: Commit — verify no TODO rows remain**

```bash
git add CLAUDE.md
git commit -m ":memo: docs(cc-concept): register learnings promotion skill in CLAUDE.md"
grep -c 'TODO: add description' CLAUDE.md || echo "0 TODO rows OK"
```

Expected: the pre-commit hook's `sync-config-table` output reports either "no changes" or an update that preserves your description (not `TODO: add description` on the new row); `0 TODO rows OK` printed after commit.

- [ ] **Step 3: Fixture A — recurring pattern detected (proves FR-080's fit criterion and the plugin-tag scope filter)**

Manual, human-in-the-loop. Seed `.claude/learnings.md` with 3+ semantically similar `[cc-concept:`-tagged entries (e.g. three entries about a client preferring a specific channel mix), plus one unrelated `[cc-concept:`-tagged one-off entry, plus at least one `[cc-content:`-tagged entry. Invoke `/cc-concept-learnings-promotion`.
Expected: the recurring group is proposed for promotion with a rationale and a proposed target; the one-off is proposed for dismissal; the `[cc-content:` entry is never mentioned anywhere in the output.
Fails if: the `[cc-content:` entry appears in the output, or the recurring group is not flagged as a pattern.

- [ ] **Step 4: Fixture B — trigger phrase non-collision (proves FR-080a)**

Manual. In a project with both `cc-concept` and `cc-content` installed, say "wrap up".
Expected: `cc-content-session-wrap` is invoked, not `cc-concept-learnings-promotion`.
Fails if: `cc-concept-learnings-promotion` triggers on any of the four session-wrap phrases.

- [ ] **Step 5: Fixture C — apply and cleanup (proves Step 4's apply/cleanup mechanics and the no-git-commits constraint)**

Manual. Using Fixture A's seeded file, approve one promotion to CLAUDE.md and one dismissal.
Expected: the approved pattern appears as prose in CLAUDE.md (not in the `## Context files` or `## Key Config Files` tables); both the promoted and dismissed entries are removed from `.claude/learnings.md`; running `git status` afterward shows the changes as unstaged — no `git add`/`git commit` was run by the skill.
Fails if: the pattern is written into either table, entries remain in `.claude/learnings.md` after approval, or any git command was executed by the skill.

- [ ] **Step 6: Fixture D — empty learnings file (proves the empty-file handling)**

Manual. Run `/cc-concept-learnings-promotion` in a project with no `.claude/learnings.md`.
Expected: the skill reports nothing to promote and stops cleanly — no error, no fabricated groups.
Fails if: the skill errors out or invents groups from nothing.

- [ ] **Step 7: Record fixture results**

After running Steps 3–6, note pass/fail for each in the session summary. Any failure is a defect in Task 1's skill file — fix there and re-run, do not paper over in the plan. Once all four fixtures pass, the five-slice `cc-concept` decomposition is complete — no further slices remain.

---
