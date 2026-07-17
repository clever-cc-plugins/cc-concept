# cc-concept Slice 1 (Foundation, Onboarding, Positioning) Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Scaffold the `cc-concept` plugin repo and ship its first two skills — coverage-driven onboarding and positioning — plus the shared contract and framework library they depend on.

**Architecture:** A standard `clever-cc-plugins` plugin repo (`marketplace/docs/cc-plugin-repo-guideline.md`). Skills are Markdown `SKILL.md` files under `plugins/cc-concept/skills/`, sharing two `_shared/` reference files. There is no compiled code and no unit-test runner; deliverables are config, shell, and Markdown files. "Tests" are therefore structural assertions (`bash -n`, JSON/YAML parse, `grep` for required sections) plus a final round of **manual fixture runs** that invoke the skills interactively (spec §5).

**Tech Stack:** Bash, JSON (plugin manifest / settings), Markdown (skills, docs), `prettier` (Markdown formatting, already the repo's PostToolUse formatter), `gitleaks` (pre-commit secret scan), `python3` (used only for JSON/YAML validity checks).

## Global Constraints

- **Design source of truth:** `docs/superpowers/specs/2026-07-16-cc-concept-foundation-design.md`. Every task traces to it.
- **Repo layout standard:** `marketplace/docs/cc-plugin-repo-guideline.md` — do not deviate.
- **Plugin name:** `cc-concept` (manifests, skill prefix). Skills invoked by bare name (`/cc-concept-onboarding`), never namespaced.
- **Copy the FIXED sync script:** `scripts/sync-config-table.sh` must be the `sync-config-table-version: 2` copy from `cc-config` (carries the trailing-padding trim + prettier-normalize-before-diff fix). Never fork or hand-edit it.
- **hooksPath is mandatory:** a fresh clone has `core.hooksPath` unset, silently disabling secret scan + table sync. Activation (`git config core.hooksPath .githooks`) is a required, verified step — not optional.
- **No secrets** committed. **No `--force`** flags. Fix root causes.
- **Do not copy skill/plugin files between repos** — the marketplace references them via `git-subdir`. The only cross-repo edit in this plan is adding one entry to `marketplace/.claude-plugin/marketplace.json` (Task 6).
- **Learnings tag format:** `[cc-concept:<skill-name>] <observation> — <YYYY-MM-DD>`.
- **Context model:** free-form `## Context files` table (`| Label | File | Summary |`); skills match on the **Summary** column semantically, never on label or filename.

---

## File Structure

Files created in this slice (all under `cc-concept/` unless noted):

| Path                                                          | Responsibility                                                   |
| ------------------------------------------------------------- | ---------------------------------------------------------------- |
| `.claude/settings.json`                                       | Baseline permissions, PreToolUse guard hook, env vars            |
| `.claude/guard-secret-files.sh`                               | PreToolUse hook: block secret `.env` reads/edits/writes (exit 2) |
| `.claude/format-markdown.sh`                                  | PostToolUse hook: prettier-format Markdown after edits           |
| `.githooks/pre-commit`                                        | gitleaks secret scan + `sync-config-table.sh`                    |
| `scripts/sync-config-table.sh`                                | FIXED v2, copied from cc-config — keeps CLAUDE.md table in sync  |
| `.gitignore`, `.claudeignore`                                 | Ignore/index-exclusion patterns                                  |
| `LICENSE`                                                     | MIT                                                              |
| `CLAUDE.md`                                                   | Project instructions + Key Config Files table                    |
| `README.md`                                                   | Install + skill overview                                         |
| `plugins/cc-concept/.claude-plugin/plugin.json`               | Plugin manifest                                                  |
| `plugins/cc-concept/skills/_shared/skill-contract.md`         | Canonical 8-step skill sequence, imported by both skills         |
| `plugins/cc-concept/skills/_shared/positioning-frameworks.md` | Curated 4-framework positioning library + selection process      |
| `plugins/cc-concept/skills/cc-concept-onboarding/SKILL.md`    | Coverage-driven context collection                               |
| `plugins/cc-concept/skills/cc-concept-positioning/SKILL.md`   | Positioning artifact generation + registration                   |
| `../marketplace/.claude-plugin/marketplace.json`              | +1 `git-subdir` entry (Task 6)                                   |

Already present: `docs/superpowers/specs/2026-07-16-cc-concept-foundation-design.md`, `docs/superpowers/plans/2026-07-17-cc-concept-slice1-foundation.md` (this file).

---

## Task 1: Repo scaffolding & hook activation

Deliverable: `cc-concept` is a valid, hook-activated plugin skeleton — all infra + manifest present, shell scripts syntactically valid, JSON valid, `hooksPath` active, and a probe commit proves the pre-commit hook populates the CLAUDE.md table.

**Files:**

- Create: `.claude/settings.json`, `.claude/guard-secret-files.sh`, `.claude/format-markdown.sh`
- Create: `.githooks/pre-commit`, `scripts/sync-config-table.sh`
- Create: `.gitignore`, `.claudeignore`, `LICENSE`, `CLAUDE.md`, `README.md`
- Create: `plugins/cc-concept/.claude-plugin/plugin.json`

**Interfaces:**

- Produces: an activated repo whose `git commit` runs `.githooks/pre-commit` → `scripts/sync-config-table.sh`, which owns the `## Key Config Files` table in `CLAUDE.md`. Later tasks rely on this table auto-updating on commit (so they never hand-edit config-file rows).

- [ ] **Step 1: Copy the three `.claude/` files and the fixed sync script verbatim from cc-config**

```bash
cd /home/michael/Git-Repos/clever-cc-plugins/cc-concept
mkdir -p .claude .githooks scripts plugins/cc-concept/.claude-plugin
cp ../cc-config/.claude/guard-secret-files.sh .claude/guard-secret-files.sh
cp ../cc-config/.claude/format-markdown.sh .claude/format-markdown.sh
cp ../cc-config/.claude/settings.json .claude/settings.json
cp ../cc-config/.githooks/pre-commit .githooks/pre-commit
cp ../cc-config/scripts/sync-config-table.sh scripts/sync-config-table.sh
chmod +x .claude/*.sh .githooks/pre-commit scripts/sync-config-table.sh
```

- [ ] **Step 2: Verify the copied sync script is the fixed v2 and scripts parse**

Run:

```bash
grep -n 'sync-config-table-version: 2' scripts/sync-config-table.sh
grep -n 'prettier --write --parser markdown "\$tmpfile"' scripts/sync-config-table.sh
for s in .claude/guard-secret-files.sh .claude/format-markdown.sh .githooks/pre-commit scripts/sync-config-table.sh; do bash -n "$s" && echo "OK $s"; done
```

Expected: version marker line prints; the prettier-normalize line prints (proves the fix is present); four `OK` lines, no syntax errors.

- [ ] **Step 3: Write `plugins/cc-concept/.claude-plugin/plugin.json`**

```json
{
  "name": "cc-concept",
  "description": "Marketing-strategy skills: positioning, competitive analysis, go-to-market, and campaign concepting",
  "author": {
    "name": "Michael van Laar"
  },
  "homepage": "https://github.com/clever-cc-plugins/cc-concept",
  "repository": "https://github.com/clever-cc-plugins/cc-concept",
  "license": "MIT"
}
```

- [ ] **Step 4: Write `.gitignore` and `.claudeignore`**

`.gitignore`:

```
.claude/settings.local.json
.claude/local.md

# Headroom — machine-local session cache and learnings
.headroom/

# MCP tool-local caches
.codegraph/
.serena/
.tokensave/
```

`.claudeignore`:

```
# Paths excluded from Claude Code indexing (add entries here as the project grows)
```

- [ ] **Step 5: Write `LICENSE` (MIT)**

Copy the MIT license text from cc-config, updating only the year/holder line to match:

```bash
cp ../cc-config/LICENSE LICENSE
grep -n 'Copyright' LICENSE
```

Expected: a `Copyright (c) ... Michael van Laar` line. If cc-config has no LICENSE file, write the standard MIT text with `Copyright (c) 2026 Michael van Laar`.

- [ ] **Step 6: Write `CLAUDE.md`**

Use this exact content. Leave the Key Config Files table with a single placeholder row — the pre-commit hook rewrites it from the filesystem on first commit.

````markdown
# cc-concept

Marketing-strategy skills for Claude Code — positioning, competitive analysis,
go-to-market planning, and campaign concepting. Distributed as a plugin via the
clever-cc-plugins marketplace. Sits upstream of `cc-content`: cc-concept sets the
strategic frame, cc-content produces the pieces that execute it.

## Key Config Files

| File        | Purpose                                    |
| ----------- | ------------------------------------------ |
| `CLAUDE.md` | Project instructions, loaded every message |

## Setup

Install from the clever-cc-plugins marketplace:

```
/plugin marketplace add clever-cc-plugins/marketplace
/plugin install cc-concept@clever-cc-plugins
```

## Don't

- Don't commit secrets or credentials to git
- Don't use `--force` flags — fix the underlying issue instead
- Don't modify CLAUDE.md directly when logging a correction — append to `.claude/learnings.md`

## Learnings

When the user corrects a mistake or points out a recurring issue, append a one-line
summary to `.claude/learnings.md`. Don't modify CLAUDE.md directly.
````

- [ ] **Step 7: Write `README.md`**

````markdown
# cc-concept

Marketing-strategy skills for Claude Code, distributed as a plugin in the
[clever-cc-plugins](https://github.com/clever-cc-plugins) family. cc-concept
produces the strategic frame — positioning, competitive analysis, go-to-market,
campaign concepts — that `cc-content` skills then execute against.

## Install

```
/plugin marketplace add clever-cc-plugins/marketplace
/plugin install cc-concept@clever-cc-plugins
```

## Skills (Slice 1)

| Skill                    | Purpose                                                                    |
| ------------------------ | -------------------------------------------------------------------------- |
| `cc-concept-onboarding`  | Collect any strategic context downstream skills need but the project lacks |
| `cc-concept-positioning` | Generate a positioning document and register it as project context         |

Skills are invoked by bare name (e.g. `/cc-concept-positioning`). cc-concept runs
standalone — it never requires `cc-content` — but recognises and reuses context an
existing `cc-content` project already provides.
````

- [ ] **Step 8: Validate JSON and stage everything**

Run:

```bash
python3 -m json.tool .claude/settings.json > /dev/null && echo "settings OK"
python3 -m json.tool plugins/cc-concept/.claude-plugin/plugin.json > /dev/null && echo "manifest OK"
git add -A
```

Expected: `settings OK` and `manifest OK`.

- [ ] **Step 9: Activate the git hooks (mandatory)**

Run:

```bash
git config core.hooksPath .githooks
git config core.hooksPath
```

Expected: prints `.githooks`. (If it prints nothing, activation failed — do not proceed.)

- [ ] **Step 10: Commit — the pre-commit hook must populate the CLAUDE.md table**

```bash
git commit -m ":tada: chore: scaffold cc-concept plugin repo"
```

Expected: pre-commit runs; `sync-config-table: updated CLAUDE.md` appears. If `gitleaks` is not installed the hook prints a warning but still proceeds.

- [ ] **Step 11: Verify the table was populated and is idempotent**

Run:

```bash
grep -c '`.claude/settings.json`' CLAUDE.md
grep -c '`plugins/cc-concept/.claude-plugin/plugin.json`' CLAUDE.md
bash scripts/sync-config-table.sh && bash scripts/sync-config-table.sh
git diff --quiet CLAUDE.md && echo "IDEMPOTENT: no churn on re-run"
```

Expected: both `grep -c` print `1` (rows were added by the hook); `IDEMPOTENT: no churn on re-run` prints (proves the padding-leak fix — the table does not grow on repeat runs). If the second command staged a CLAUDE.md change, `git add CLAUDE.md && git commit --amend --no-edit` and re-run this step.

---

## Task 2: Shared skill contract

Deliverable: `_shared/skill-contract.md` — the single canonical 8-step sequence both skills import by reference, so the sequence is never duplicated (the anti-drift purpose, spec §3.1 / NFR-031).

**Files:**

- Create: `plugins/cc-concept/skills/_shared/skill-contract.md`

**Interfaces:**

- Produces: a file referenced by `cc-concept-onboarding/SKILL.md` and `cc-concept-positioning/SKILL.md` (Tasks 4–5). Both cite it by relative path and add only skill-specific behavior.

- [ ] **Step 1: Write `_shared/skill-contract.md`**

The file must open with a one-paragraph framing ("Every cc-concept skill follows this sequence; a SKILL.md references this file rather than restating it") and then the eight numbered steps **verbatim** as below:

```markdown
# cc-concept Skill Contract — Shared Reference

Every cc-concept skill follows the same step sequence. A SKILL.md **references this
file** rather than restating the sequence — this is the single source of truth, so
the steps cannot drift skill to skill. A skill documents only its own specifics:
what it gates on, what it generates, and where it writes.

## The sequence

0. **Recall learnings** (silent) — read `.claude/learnings.md` if present, across
   all plugin tags. Apply relevant observations. Never announce this step; surface
   nothing unless it changes behavior.
1. **Load context** — read the `## Context files` table in `CLAUDE.md`. Match needs
   against the **Summary** column semantically — never against a label or filename.
2. **Briefing check** — confirm the skill has the context it needs. Warn only on the
   _semantic absence_ of a required content-need, never on a missing label.
3. **Calibrate** — set depth and scope from the request and the context available.
4. **Generate** — produce the artifact against the relevant `_shared/` reference.
5. **Internal quality check** — self-review before showing anything.
6. **Delimited output** — return the artifact inside clear delimiters.
7. **Two-phase feedback** — auto-store lightweight learnings (tagged
   `[cc-concept:<skill-name>]`); ask before promoting anything heavier.
```

- [ ] **Step 2: Verify structure**

Run:

```bash
f=plugins/cc-concept/skills/_shared/skill-contract.md
for n in 0. 1. 2. 3. 4. 5. 6. 7.; do grep -q "^$n \*\*" "$f" && echo "step $n OK"; done
grep -q 'Summary' "$f" && grep -q 'semantic absence' "$f" && echo "context rules OK"
```

Expected: eight `step N OK` lines and `context rules OK`.

- [ ] **Step 3: Commit**

```bash
git add plugins/cc-concept/skills/_shared/skill-contract.md
git commit -m ":memo: feat(cc-concept): add shared skill contract"
```

---

## Task 3: Positioning framework library

Deliverable: `_shared/positioning-frameworks.md` — a curated, domain-scoped library of exactly four positioning frameworks plus an explicit selection process carrying the project-override rule (spec §4 / FR-081, FR-082, FR-083). Mirrors the shape of `cc-content/plugins/cc-content/skills/_shared/storytelling-frameworks.md`.

**Files:**

- Create: `plugins/cc-concept/skills/_shared/positioning-frameworks.md`
- Reference (read for shape, do not modify): `cc-content/plugins/cc-content/skills/_shared/storytelling-frameworks.md`

**Interfaces:**

- Produces: the reference `cc-concept-positioning` generates against (Task 5). The positioning skill states its framework choice from this file before generating.

- [ ] **Step 1: Read the shape reference**

Run:

```bash
sed -n '1,45p' ../cc-content/plugins/cc-content/skills/_shared/storytelling-frameworks.md
```

Expected: shows the framing intro + "How to select a framework" numbered process + per-framework entry format (name / one-line / best-for / avoid). Mirror this shape.

- [ ] **Step 2: Write `_shared/positioning-frameworks.md`**

The file must contain, in order:

1. **Framing intro** — this library is for positioning/differentiation work; when to apply it, when a task is too small to need it.
2. **"How to select a framework"** — a numbered process ending in a stated choice: `> "Using the [framework] because [one-sentence reason]."` The process must include the **project-override rule** verbatim in spirit: _"If the project's registered context states a preferred positioning approach (e.g. 'always Jobs-to-be-Done, never Porter's Five Forces'), that preference wins over this file's default — do not edit this file to encode it."_
3. **Four framework entries**, each with the same fields — **What it is / Best for / Avoid / How to apply**:
   - **April Dunford — Obviously Awesome** — positioning as deliberate competitive context (competitive alternatives → unique attributes → value → best-fit customer → market frame).
   - **Geoffrey Moore — Positioning Statement Template** — the fill-in template: _For [target] who [need], [product] is a [category] that [benefit]. Unlike [alternative], our product [differentiator]._
   - **Value Proposition Canvas** — customer profile (jobs / pains / gains) mapped to value map (products / pain relievers / gain creators).
   - **Perceptual Map** — two-axis plot of competitors to find open, ownable space.

- [ ] **Step 3: Verify the four frameworks, selection process, and override rule are all present**

Run:

```bash
f=plugins/cc-concept/skills/_shared/positioning-frameworks.md
grep -q 'Dunford' "$f" && grep -q 'Moore' "$f" && grep -q 'Value Proposition Canvas' "$f" && grep -q -i 'perceptual map' "$f" && echo "4 frameworks OK"
grep -q -i 'how to select' "$f" && echo "selection process OK"
grep -q -i 'override\|wins over\|preferred' "$f" && echo "override rule OK"
```

Expected: `4 frameworks OK`, `selection process OK`, `override rule OK`.

- [ ] **Step 4: Commit**

```bash
git add plugins/cc-concept/skills/_shared/positioning-frameworks.md
git commit -m ":memo: feat(cc-concept): add positioning framework library"
```

---

## Task 4: Onboarding skill

Deliverable: `cc-concept-onboarding/SKILL.md` — coverage-driven context collection that fills **every** gated need not already covered (spec §3.2). For Slice 1 the gated needs are organization background and competitive landscape (positioning's two needs, Task 5).

**Files:**

- Create: `plugins/cc-concept/skills/cc-concept-onboarding/SKILL.md`
- Reference (read for shape): `cc-content/plugins/cc-content/skills/cc-content-onboarding/SKILL.md`
- Depends on: `_shared/skill-contract.md` (Task 2)

**Interfaces:**

- Consumes: the `## Context files` table Summary column; the shared contract's step sequence.
- Produces: new context files (own file each, collision-checked filename) registered as `| Label | File | Summary |` rows. Guarantees that after a run, every gated need is either pre-covered or newly collected.

- [ ] **Step 1: Read the shape reference**

Run: `sed -n '1,60p' ../cc-content/plugins/cc-content/skills/cc-content-onboarding/SKILL.md`
Expected: frontmatter (`name`, folded `description:` with trigger phrases, `allowed-tools`, `argument-hint`) then `# ... Skill`, `## Step 0: Recall learnings`, etc. Mirror this frontmatter and heading style.

- [ ] **Step 2: Write the SKILL.md frontmatter**

```markdown
---
name: cc-concept-onboarding
description: >
  Use this skill to set up or extend the strategic context a marketing project needs
  before positioning, competitive, or go-to-market work. Invoke when the user asks to
  "onboard for strategy", "set up strategy context", "add competitive context", or when
  a cc-concept skill reports a missing strategic need. Runs standalone and also
  recognises context an existing cc-content project already provides.
allowed-tools: Read, Write, Edit, Bash
argument-hint: "[optional: path to an existing file to register as strategic context]"
---
```

- [ ] **Step 3: Write the skill body**

Body must contain, in order:

1. A one-paragraph intro: this skill collects the strategic context downstream cc-concept skills need; context files are registered in the `## Context files` table; skills load them on demand.
2. **A reference to the contract**, not a restatement: `This skill follows the shared step sequence in ../_shared/skill-contract.md. Steps below add only onboarding-specific behavior.`
3. **Step 0 (Recall learnings)** — per contract; silent.
4. **Step 1 (Discover existing context)** — scan for `CLAUDE.md` files and existing `## Context files` tables (mirror cc-content-onboarding's `find` scan). Read the Summary column of every registered row.
5. **Step 2 (Coverage check — the core logic):** For each gated need in `{organization background, competitive landscape}`, decide **covered / uncovered** by semantic match against the Summary column — **not** by filename and **not** by whether onboarding ran before (coverage detection, not run detection, FR-011). The two needs are evaluated **independently** — one covered does not exempt the other. Explicitly: in a cc-content project, organization background is typically already covered → skip it; competitive landscape is not (cc-content never collects it) → collect it. In a bare project both are uncovered → collect both.
6. **Step 3 (Collect):** For each uncovered need, run a short guided interview (or register a passed-in file if `$ARGUMENTS` is a path). Write each need to **its own file** with a **collision-checked** name (never overwrite an existing context file — if the target name exists, pick a distinct one), by convention under `context/` but the table is the source of truth (CON-004).
7. **Step 4 (Register):** Add a `| Label | File | Summary |` row per new file with a semantic Summary describing the need it covers. Do **not** hand-edit the Key Config Files table (the pre-commit hook owns that).
8. **Step 7 (Feedback):** per contract; store learnings tagged `[cc-concept:cc-concept-onboarding]`.

- [ ] **Step 4: Verify frontmatter validity and required behavior markers**

Run:

```bash
f=plugins/cc-concept/skills/cc-concept-onboarding/SKILL.md
python3 - "$f" <<'PY'
import sys, yaml
t = open(sys.argv[1]).read().split('---')
meta = yaml.safe_load(t[1])
assert meta['name'] == 'cc-concept-onboarding', meta.get('name')
assert 'description' in meta and 'allowed-tools' in meta
print("frontmatter OK")
PY
grep -q 'skill-contract.md' "$f" && echo "contract ref OK"
grep -q -i 'competitive landscape' "$f" && grep -q -i 'organization background' "$f" && echo "both needs OK"
grep -q -i 'collision\|already exists\|do not overwrite\|never overwrite' "$f" && echo "collision-check OK"
grep -q -i 'independently\|each.*need\|one being covered' "$f" && echo "independent-eval OK"
```

Expected: `frontmatter OK`, `contract ref OK`, `both needs OK`, `collision-check OK`, `independent-eval OK`.

- [ ] **Step 5: Commit**

```bash
git add plugins/cc-concept/skills/cc-concept-onboarding/SKILL.md
git commit -m ":sparkles: feat(cc-concept): add coverage-driven onboarding skill"
```

---

## Task 5: Positioning skill

Deliverable: `cc-concept-positioning/SKILL.md` — generates a positioning document against the framework library, gating on organization background + competitive landscape with the three-state model, and registers the output as project context (spec §3.3).

**Files:**

- Create: `plugins/cc-concept/skills/cc-concept-positioning/SKILL.md`
- Depends on: `_shared/skill-contract.md` (Task 2), `_shared/positioning-frameworks.md` (Task 3)

**Interfaces:**

- Consumes: the `## Context files` table (org background + competitive landscape Summaries); `_shared/positioning-frameworks.md`; the shared contract.
- Produces: `context/brand-positioning.md` (collision-checked) + a `## Context files` row, consumable by later cc-concept and cc-content skills.

- [ ] **Step 1: Write the SKILL.md frontmatter**

```markdown
---
name: cc-concept-positioning
description: >
  Use this skill to develop or refine product/company positioning — how the offering is
  differentiated, for whom, against which alternatives. Invoke when the user asks to
  "work on positioning", "define our positioning", "write a positioning statement",
  "differentiate us from competitors", or "position the product". Produces a positioning
  document and registers it as project context.
allowed-tools: Read, Write, Edit, Bash
argument-hint: "[optional: brief or focus for the positioning work]"
---
```

- [ ] **Step 2: Write the skill body**

Body must contain, in order:

1. Intro: this skill produces a positioning document — the strategic frame downstream content executes against.
2. **Contract reference:** `This skill follows the shared step sequence in ../_shared/skill-contract.md. Steps below add only positioning-specific behavior.`
3. **Step 0–1** per contract (recall learnings; load the `## Context files` table by Summary).
4. **Step 2 (Gating — three-state model):** Gate on **exactly two** needs — **organization background** and **competitive landscape**. Audience, language, and format preferences are noted silently if present and never block. For each gated need resolve one of three states:
   - **covered** — present in the context table (Summary match) → use silently, no ask;
   - **absent-but-supplied** — ask **once** (NFR-011, never twice in one invocation), user answers → use, non-degraded;
   - **absent-and-unanswered** — asked once, no usable answer → the corresponding section is labelled **⚠ DEGRADED** (FR-004), never fabricated, and the rest of the document still generates.
5. **Step 3 (Calibrate)** per contract.
6. **Step 4 (Generate):** select a framework from `../_shared/positioning-frameworks.md` following that file's selection process, **state the choice** (`Using the [framework] because …`) before generating, then produce the positioning document.
7. **Step 5–6 (Quality check + delimited output)** per contract.
8. **Register output:** write to `context/brand-positioning.md` by convention, **collision-checked** (if it exists, choose a distinct non-colliding name — must not collide with or be mistaken for the organization-profile convention, NFR-040), and add a `| Label | File | Summary |` row.
9. **Step 7 (Feedback):** store learnings tagged `[cc-concept:cc-concept-positioning]`.

- [ ] **Step 3: Verify frontmatter and the gating/degradation/framework markers**

Run:

```bash
f=plugins/cc-concept/skills/cc-concept-positioning/SKILL.md
python3 - "$f" <<'PY'
import sys, yaml
meta = yaml.safe_load(open(sys.argv[1]).read().split('---')[1])
assert meta['name'] == 'cc-concept-positioning', meta.get('name')
assert 'allowed-tools' in meta
print("frontmatter OK")
PY
grep -q 'skill-contract.md' "$f" && echo "contract ref OK"
grep -q 'positioning-frameworks.md' "$f" && echo "library ref OK"
grep -q -i 'organization background' "$f" && grep -q -i 'competitive landscape' "$f" && echo "two needs OK"
grep -q -i 'DEGRADED' "$f" && grep -q -i 'once' "$f" && echo "three-state OK"
grep -q -i 'collision\|distinct.*name\|must not collide\|never overwrite' "$f" && echo "collision-check OK"
```

Expected: `frontmatter OK`, `contract ref OK`, `library ref OK`, `two needs OK`, `three-state OK`, `collision-check OK`.

- [ ] **Step 4: Commit**

```bash
git add plugins/cc-concept/skills/cc-concept-positioning/SKILL.md
git commit -m ":sparkles: feat(cc-concept): add positioning skill"
```

---

## Task 6: Marketplace registration & fixture verification

Deliverable: cc-concept is registered in the marketplace catalog, and the three verification scenarios from spec §5 pass with the skills invoked for real.

**Files:**

- Modify: `../marketplace/.claude-plugin/marketplace.json` (add one `git-subdir` entry)
- Reference: spec §5

**Interfaces:**

- Consumes: the two committed skills (Tasks 4–5) and both `_shared/` files (Tasks 2–3).

- [ ] **Step 1: Add the marketplace entry**

In `marketplace/.claude-plugin/marketplace.json`, add to the plugins array (matching the existing entries' shape and trailing-comma/formatting conventions):

```json
{
  "name": "cc-concept",
  "source": {
    "source": "git-subdir",
    "url": "https://github.com/clever-cc-plugins/cc-concept.git",
    "path": "plugins/cc-concept"
  },
  "description": "Marketing-strategy skills: positioning, competitive analysis, go-to-market, and campaign concepting"
}
```

- [ ] **Step 2: Validate the catalog JSON and commit it in the marketplace repo**

Run:

```bash
cd ../marketplace
python3 -m json.tool .claude-plugin/marketplace.json > /dev/null && echo "catalog JSON OK"
python3 -c "import json;print([p['name'] for p in json.load(open('.claude-plugin/marketplace.json'))['plugins']])"
git add .claude-plugin/marketplace.json
git commit -m ":heavy_plus_sign: feat: register cc-concept in marketplace catalog"
cd ../cc-concept
```

Expected: `catalog JSON OK`; the printed name list includes `cc-concept`.

- [ ] **Step 3: Fixture A — bare project (proves Approach A / NFR-041)**

Manual, human-in-the-loop. In a fresh scratch project with **no** context, invoke `/cc-concept-onboarding` then `/cc-concept-positioning`.
Expected: onboarding detects **both** gated needs uncovered and collects both; positioning then finds both covered, runs **ungated** (no asks, no degraded sections), writes a collision-checked `context/brand-positioning.md`, and registers a `## Context files` row.
Fails if: onboarding collects only one need and positioning is still gated/degraded on the other.

- [ ] **Step 4: Fixture B — cc-content-onboarded project (proves FR-011 / FR-021 / FR-002a / NFR-040)**

Manual. In a scratch project already carrying `company-profile.md` + brand-voice + audience rows in the `## Context files` table (org background covered, competitive landscape **not**), invoke onboarding then positioning.
Expected: onboarding recognises organization background is covered (Summary match, not filename) and does **not** re-collect it, detects competitive landscape uncovered and collects only that; positioning consumes existing profile + new competitive context and produces a **non-degraded** artifact whose file does not collide with the org-profile file.
Fails if: onboarding re-asks for org background, or skips the uncovered competitive need, or positioning ignores the profile.

- [ ] **Step 5: Negative test — positioning alone, competitive absent (proves NFR-011 / FR-004)**

Manual. In a project where org background is covered but competitive landscape is absent, invoke `/cc-concept-positioning` **without** onboarding first, and give no usable answer when asked.
Expected: positioning asks **once** for competitive input; with no usable answer it labels the competitive section **⚠ DEGRADED** (not fabricated) and still generates the rest.
Fails if: it asks repeatedly, silently fabricates, or hard-errors.

- [ ] **Step 6: Record fixture results**

After running Steps 3–5, note pass/fail for each in the session summary. Any failure is a defect in the responsible task's skill file — fix there and re-run, do not paper over in the plan.

---

## Deferred to end of Slice 1 (not a task above)

Once both skills pass their fixtures, write `../cc-content/docs/shared-contract-refactor.md`: a short instruction doc describing how to migrate cc-content onto an equivalent `_shared/skill-contract.md`. It must call out that **`cc-content-new-skill` generates skills**, so the generator must emit skills that _import_ the contract rather than restate it — otherwise the drift the contract prevents reappears through the generator. This doc is written, not executed, in Slice 1.
