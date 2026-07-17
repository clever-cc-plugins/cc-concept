# cc-concept — Slice 1 Design: Foundation, Onboarding, and Positioning

**Status:** Approved for implementation
**Date:** 2026-07-16
**Source briefing:** `requirements-cc-concept.md` (v2.1)
**Scope:** Slice 1 of 5 (foundation + onboarding + positioning)

---

## 1. Purpose and scope

`cc-concept` is a Claude Code plugin in the `clever-cc-plugins` ecosystem for
**marketing-strategy work** — positioning, competitive analysis, go-to-market
planning, and campaign concepting. It sits upstream of `cc-content`: where
`cc-content` produces individual pieces of content, `cc-concept` produces the
strategic frame those pieces execute against.

This document specifies **Slice 1 only**. Slice 1 delivers a working plugin with
two skills — onboarding and positioning — plus the shared infrastructure both
depend on. It is the smallest slice that proves the plugin's core contract end to
end: collect strategic context, generate a strategy artifact against curated
frameworks, and hand the result forward as reusable project context.

### 1.1 The five-slice decomposition (context)

| Slice | Delivers                                                  |
| ----- | --------------------------------------------------------- |
| **1** | **Foundation + onboarding + positioning** (this document) |
| 2     | Campaign-concept skill + brief.md handoff to cc-content   |
| 3     | Advisor skills (channel advisor, marketing advisor)       |
| 4     | Planning skills (content-strategy, go-to-market)          |
| 5     | Learnings-promotion skill (narrow, own trigger)           |

Slices 2–5 are out of scope here and are named only to justify Slice 1's
extension points (the shared contract, the framework-library shape, the
learnings tags). Nothing in Slice 1 may hard-code assumptions that block a later
slice, but no later-slice code is written now.

---

## 2. Repository foundation

The repo already exists as an empty clone at
`/home/michael/Git-Repos/clever-cc-plugins/cc-concept`
(remote `git@github.com:clever-cc-plugins/cc-concept.git`, default branch `main`,
`core.hooksPath` currently **unset**). Slice 1 scaffolds it to the standard
plugin-repo layout defined in
`marketplace/docs/cc-plugin-repo-guideline.md`.

### 2.1 Target tree

```
cc-concept/
├── .claude/
│   ├── settings.json
│   ├── guard-secret-files.sh
│   └── format-markdown.sh
├── .githooks/
│   └── pre-commit
├── scripts/
│   └── sync-config-table.sh          # copy the FIXED v2 from cc-config
├── docs/
│   └── superpowers/specs/
│       └── 2026-07-16-cc-concept-foundation-design.md   # this file
├── plugins/
│   └── cc-concept/
│       ├── .claude-plugin/
│       │   └── plugin.json
│       └── skills/
│           ├── _shared/
│           │   ├── skill-contract.md
│           │   └── positioning-frameworks.md
│           ├── cc-concept-onboarding/
│           │   └── SKILL.md
│           └── cc-concept-positioning/
│               └── SKILL.md
├── .claudeignore
├── .gitignore
├── CLAUDE.md
├── LICENSE                            # MIT
└── README.md
```

### 2.2 Scaffolding rules

- **Copy the FIXED `sync-config-table.sh`** from `cc-config` (version marker
  `sync-config-table-version: 2`) — it carries the trailing-padding trim and the
  prettier-normalize-before-diff fix. Do **not** copy an older forked variant.
- **`.githooks/pre-commit`** is the standard gitleaks + table-sync hook. After
  scaffolding, activate it explicitly:
  `chmod +x .githooks/pre-commit && git config core.hooksPath .githooks`.
  This step is **mandatory and easy to forget** — a fresh clone has `hooksPath`
  unset, which silently disables both secret scanning and table sync. Slice 1 is
  not complete until `git config core.hooksPath` returns `.githooks`.
- **`.claude/settings.json`** uses the baseline permissions + PreToolUse guard
  hook from the guideline. No plugin-specific permission changes are needed in
  Slice 1.
- **`plugins/cc-concept/.claude-plugin/plugin.json`** follows the standard
  manifest shape (`name: cc-concept`, homepage/repository pointing at the
  `clever-cc-plugins/cc-concept` repo, MIT license).
- **Marketplace registration** is a **separate `git-subdir` entry** added to
  `marketplace/.claude-plugin/marketplace.json` pointing at
  `plugins/cc-concept`. No files move; the entry is added in the `marketplace`
  repo, not here. This is done as the final commit of Slice 1.

---

## 3. The two skills

### 3.1 Shared skill contract — `_shared/skill-contract.md`

Both skills (and every later-slice skill) follow the same step sequence
(briefing NFR-031). Rather than duplicate that sequence into each SKILL.md — the
duplication that produced today's real drift bug in `cc-content-new-skill` — the
sequence is **factored into one file** that each SKILL.md imports by reference.

The contract file defines the canonical step order:

0. **Recall learnings** (silent) — read `.claude/learnings.md`, all plugin tags,
   apply relevant observations. Never surfaced unless it changes behavior.
1. **Load context** — read the `## Context files` table in `CLAUDE.md`; match on
   the **Summary** column semantically, not on labels or filenames.
2. **Briefing check** — confirm the skill has what it needs; warn only on the
   _semantic absence_ of a required content-need, never on a missing label.
3. **Calibrate** — set depth/scope from the request and available context.
4. **Generate** — produce the artifact against the relevant `_shared/` reference.
5. **Internal quality check** — self-review before showing output.
6. **Delimited output** — return the artifact inside clear delimiters.
7. **Two-phase feedback** — auto-store lightweight learnings; ask before
   promoting anything heavier.

Each SKILL.md references this file instead of restating the sequence, and adds
only its skill-specific behavior (what it gates on, what it generates, where it
writes). **Extension point:** `cc-content` will later import an equivalent
contract; a short migration note for that is written at the _end_ of Slice 1
(see §6), once the contract has been proven by two working skills here.

### 3.2 `cc-concept-onboarding`

**Role:** coverage-driven context collection (briefing FR-011, FR-012;
"Approach A").

Onboarding collects **every gated strategic need not already covered** by
existing project context. For Slice 1 the only downstream skill is positioning,
whose gated needs are **organization background** and **competitive landscape**
(§3.3) — so those are exactly the two needs onboarding is responsible for
covering. It is _supplemental_: in a project already onboarded by `cc-content`
(which has a `company-profile.md`, brand voice, audience files), organization
background is already covered, so onboarding collects only the remaining
uncovered need — competitive landscape — and stays quiet about the rest. In a
**bare** project it collects **both** needs from scratch, so that positioning is
never permanently degraded.

Key rules:

- **Coverage detection, not run detection** (FR-011): onboarding decides what to
  collect by checking whether each gated need is _semantically covered_ in the
  existing context table, not by whether onboarding has "been run before." Both
  gated needs are evaluated independently — one being covered does not exempt the
  other.
- It does **not** blindly re-collect what `cc-content` onboarding already
  established; overlap is detected via the Summary column and skipped.
- Each context file it creates is written to its **own file** (per the
  "always its own file" decision, 2026-07-16), with a **collision-checked**
  filename (never overwrite an existing context file), and
  registered as a row in the `## Context files` table with a semantic Summary.
- `context/` is the **convention**, not a mandate (CON-004) — the table is the
  source of truth, not the directory.

### 3.3 `cc-concept-positioning`

**Role:** generate a positioning artifact and hand it forward as project context.

- **Gating (OQ-007, decided):** positioning gates on **two** needs only —
  **organization background** and **competitive landscape**. Audience, language,
  and format preferences are noted silently if present and never block.
- For each gated need there are three states: **covered** (present in the context
  table → used silently, no ask); **absent-but-supplied** (asked **once** per
  NFR-011, user answers → used, non-degraded); **absent-and-unanswered** (asked
  once, no usable answer → section labelled **⚠ DEGRADED** per FR-004, never
  fabricated). Positioning is only fully non-degraded when **both** needs reach
  covered or absent-but-supplied.
- It generates against `_shared/positioning-frameworks.md` (see §4), **stating
  its framework choice** before generating (mirroring the storytelling-frameworks
  selection ritual).
- Output is written to its **own, collision-checked** context file
  (`context/brand-positioning.md` by convention) and registered in the
  `## Context files` table so downstream `cc-concept` and `cc-content` skills can
  consume it.
- In a bare project, onboarding (§3.2) will have collected **both** gated needs
  first, so positioning finds both covered and runs **ungated** (no asks, no
  degraded sections) — this is the end-to-end path Fixture A verifies (§5).

---

## 4. Framework library — `_shared/positioning-frameworks.md`

A **curated, domain-scoped** reference file (briefing FR-081 "domain-scoped
files", FR-083 "start small"). It mirrors the shape of
`cc-content`'s `storytelling-frameworks.md`:

1. A **framing intro** — when to apply the file, when to skip it.
2. An **explicit selection process** — how to pick a framework for the task,
   ending in a stated choice ("Using the [framework] because …"). The selection
   process carries the **project-override rule** (FR-082): if the project's
   context supplies its own positioning approach, prefer it over the library
   default.
3. **Four framework entries**, each with the same fields
   (what it is / best for / avoid / how to apply):
   - **April Dunford — Obviously Awesome** (positioning as competitive context)
   - **Geoffrey Moore — positioning statement template** (For / Who / Our
     product / That / Unlike / Our product)
   - **Value Proposition Canvas** (jobs / pains / gains ↔ products / pain
     relievers / gain creators)
   - **Perceptual map** (two-axis competitive differentiation)

Four is deliberately small (FR-083). The file's shape — framing + selection +
uniform entries — is the extension point later slices add frameworks to without
restructuring.

---

## 5. Verification

Slice 1 is verified **manually** against two fixture projects plus one negative
test. This exercises the real skill paths rather than asserting "no error"
(NFR-041 means _actually works_, not _exits cleanly_).

### Fixture A — bare project (proves Approach A / NFR-041)

A fresh project with **no** existing context. Run onboarding, then positioning.

- **Expect:** onboarding detects that **both** gated needs — organization
  background and competitive landscape — are uncovered and collects both;
  positioning then finds both covered, runs **ungated** (no asks, no degraded
  sections), and produces a non-degraded positioning artifact written to a
  collision-checked context file and registered in the table.
- **Fails if:** onboarding collects only one need and positioning is then still
  gated/degraded on the other (would mean coverage-driven collection does not
  cover every gated need — the exact failure Approach A exists to prevent).

### Fixture B — cc-content-onboarded project (proves FR-011 / FR-021 / FR-002a / NFR-040)

A project already carrying `company-profile.md`, a brand-voice file, and audience
files registered in the `## Context files` table — i.e. organization background
is covered, competitive landscape is **not** (cc-content never collects it). Run
onboarding, then positioning.

- **Expect:** onboarding recognises organization background is already covered
  (via Summary matching, not filename) and does **not** re-collect it, but
  detects competitive landscape is uncovered and collects only that; positioning
  then consumes the existing company profile plus the newly collected competitive
  context and produces a non-degraded artifact.
- **Fails if:** onboarding re-asks for organization background (overlap detection
  broken), or fails to collect the uncovered competitive need, or positioning
  ignores the existing company profile.

### Negative test — positioning alone, competitive absent (proves NFR-011 / FR-004)

Run positioning **directly, without onboarding first**, on a project where
organization background is covered but competitive landscape is absent, and give
no usable answer when asked.

- **Expect:** positioning asks **once** (NFR-011) for the competitive input; with
  no usable answer, the competitive section is labelled **⚠ DEGRADED** (FR-004)
  rather than fabricated, and the rest of the artifact still generates.
- **Fails if:** it asks repeatedly, silently fabricates, or hard-errors.

---

## 6. Deferred to end of Slice 1

After both skills are working and the shared contract is proven, write a short
instruction doc in **cc-content** (`docs/shared-contract-refactor.md`) describing
how to migrate `cc-content` onto an equivalent `_shared/skill-contract.md`. It
must call out that **`cc-content-new-skill` generates skills**, so the generator
must emit new skills that import the contract rather than restate it — otherwise
the drift bug the contract exists to prevent reappears through the generator.

This doc is **written, not executed** in Slice 1; the cc-content refactor is a
separate future task.

---

## 7. Traceability to the briefing

| Decision (this doc)                          | Briefing ref            |
| -------------------------------------------- | ----------------------- |
| Standalone core, onboarding supplemental     | OQ-001, FR-012          |
| Coverage-driven onboarding (Approach A)      | FR-011, NFR-041         |
| Positioning gates on org bg + competitive    | OQ-007, FR-004, NFR-011 |
| Own collision-checked output file            | FR-022, CON-004         |
| Free-form Summary matching                   | FR-002, FR-002a         |
| Curated, domain-scoped, small framework lib  | FR-081, FR-082, FR-083  |
| Own narrow learnings-promotion skill (later) | OQ-003, FR-080          |
| Name = cc-concept                            | OQ-008                  |
| Shared contract factored into `_shared/`     | NFR-031 (anti-drift)    |

**Still open (not blocking Slice 1):** OQ-005 (advisor output shape — Slice 3),
OQ-006 (delineation vs `cc-content-ideation`/`-text` — revisit at Slice 2 brief
handoff).
