<b>English</b> · <a href="README.zh-CN.md">简体中文</a>

# Skills

A personal collection of agent skills for day-to-day work on this machine. Nothing here is published, and the repo does not aim for parity with upstream.

Sources: most skills derive from [mattpocock/skills](https://github.com/mattpocock/skills) `v1.3.2`, `redesign-existing-projects` derives from [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill) `v2.1.0`, and `find-skills` derives from [vercel-labs/skills](https://github.com/vercel-labs/skills) at commit `57217cf` (that repository publishes no tags). Per-skill sources, upstream paths and commits are in [NOTICE.md](./NOTICE.md); the actual deltas against upstream are in [patches/](./patches/README.md).

The localisation follows one principle: upstream treats an issue tracker (GitHub or GitLab Issues plus a triage label scheme) as prerequisite infrastructure, and this repo removes that dependency, keeping only the path built on local markdown and domain docs. Skills that need a tracker or operations outside the repo are therefore excluded: `triage`, `wayfinder`, `wizard`, `pr` and `to-questionnaire`. `to-tickets` sat in that group originally, but it has been rewritten against local markdown tickets (`.scratch/<feature>/issues/`) and reintroduced.

## Overview

| Item | Count | Notes |
| --- | --- | --- |
| Skills | 24 | 17 in `engineering`, 7 in `productivity` |
| User-invoked | 14 | Triggered only by a human typing `/skill-name` |
| Model-invoked | 10 | The model may trigger them at its own discretion |
| Listed in the plugin manifest | 24 | One entry per skill directory on disk |
| Files changed from upstream with a patch | 17 | 13 markdown files and 4 `agents/openai.yaml`, see `patches/` |

## Repository layout

```text
.
├── CLAUDE.md                    Repo conventions, binding for maintainers and agents
├── AGENTS.md                    Symlink to CLAUDE.md; both names serve the same rules
├── README.md                    English version (this file)
├── README.zh-CN.md              Simplified Chinese version
├── NOTICE.md                    Skill sources, upstream paths and commits
├── LICENSE                      MIT
├── package.json                 Entry point for changesets and the version sync script
├── .agents/
│   └── invocation.md            Invocation types and cross-skill call rules
├── .changeset/
│   └── config.json              Release configuration
├── .claude-plugin/
│   ├── marketplace.json         Marketplace entry (georgewuw)
│   └── plugin.json              Plugin manifest; the skills array decides what ships with the plugin
├── patches/
│   ├── README.md                Patch baseline, inventory, how to apply and regenerate
│   ├── leonxlnx-taste-skill-v2.1.0/   1 patch, paths mirroring upstream paths
│   ├── mattpocock-skills-v1.3.2/      15 patches, paths mirroring upstream paths
│   └── vercel-labs-skills-57217cf/    1 patch, paths mirroring upstream paths
├── scripts/
│   ├── link-skills.sh           Symlinks skills into ~/.claude/skills and ~/.agents/skills
│   ├── list-skills.sh           Lists every SKILL.md in the repo
│   └── sync-plugin-version.mjs  Writes the package.json version into plugin.json
└── skills/
    ├── engineering/             Day-to-day coding work
    │   ├── README.md
    │   ├── ask-help/            SKILL.md, PHASE-BOUNDARIES.md, agents/openai.yaml
    │   ├── code-review/
    │   ├── codebase-design/     SKILL.md, DEEPENING.md, DESIGN-IT-TWICE.md, agents/openai.yaml
    │   ├── diagnosing-bugs/     SKILL.md, agents/openai.yaml, scripts/hitl-loop.template.sh
    │   ├── domain-modeling/     SKILL.md, ADR-FORMAT.md, GLOSSARY-FORMAT.md, agents/openai.yaml
    │   ├── grill-with-docs/
    │   ├── implement/
    │   ├── implement-spec/
    │   ├── improve-codebase-architecture/  SKILL.md, HTML-REPORT.md, agents/openai.yaml
    │   ├── project-preset-for-skills/      SKILL.md, domain.md, agents/openai.yaml
    │   ├── prototype/           SKILL.md, LOGIC.md, UI.md, agents/openai.yaml
    │   ├── redesign-existing-projects/
    │   ├── research/
    │   ├── retro/
    │   ├── tdd/                 SKILL.md, mocking.md, tests.md, agents/openai.yaml
    │   ├── to-spec/
    │   └── to-tickets/          SKILL.md, agents/openai.yaml
    └── productivity/            Everyday non-coding workflows
        ├── README.md
        ├── find-skills/
        ├── grill-me/
        ├── grilling/
        ├── handoff/
        ├── teach/               SKILL.md, MISSION-FORMAT.md, RESOURCES-FORMAT.md,
        │                        LEARNING-RECORD-FORMAT.md, GLOSSARY-FORMAT.md, agents/openai.yaml
        ├── wait-what/
        └── writing-for-agents/  SKILL.md, SKILL-MECHANICS.md, agents/openai.yaml
```

Every skill directory carries `agents/openai.yaml` (Codex UI metadata; user-invoked skills also carry `policy.allow_implicit_invocation: false`). The tree expands multi-file skills only; single-file skills are not listed file by file.

## Skills

Source column abbreviations:

- `v1.3.2`: [mattpocock/skills](https://github.com/mattpocock/skills) tag `v1.3.2`, commit `d1478fcb140db0b93c0c8df17bcfd311844749d0`.
- `taste-skill v2.1.0`: [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill) tag `v2.1.0`, commit `a206bbf75a9d80554c0de17c1198ee2fbbc555aa`.
- `57217cf`: [vercel-labs/skills](https://github.com/vercel-labs/skills) commit `57217cf86ba38148a57af9e90d14a4c049558330`. No tags upstream, so the baseline is that commit and never a branch head.
- `as-is`: byte-identical to the upstream file. `patched`: content trimmed, change recorded in `patches/`.

### Engineering (17)

User-invoked:

| Skill | Purpose | Source |
| --- | --- | --- |
| [ask-help](./skills/engineering/ask-help/SKILL.md) | Routing entry: recommends the skill and flow for your situation | v1.3.2 / `engineering/ask-matt` (renamed, patched) |
| [grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md) | Continuous questioning around a design, settling terms into `GLOSSARY.md` and ADRs as it goes | v1.3.2 / `engineering/grill-with-docs` (as-is) |
| [improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md) | Scans a codebase for module-deepening opportunities, produces an HTML report, then grills the chosen one | v1.3.2 / `engineering/improve-codebase-architecture` (as-is) |
| [to-spec](./skills/engineering/to-spec/SKILL.md) | Synthesises the current conversation into a spec; no interview, nothing published to a tracker | v1.3.2 / `engineering/to-spec` (patched) |
| [to-tickets](./skills/engineering/to-tickets/SKILL.md) | Splits a plan, spec or conversation into tracer-bullet tickets that declare their blocking edges, one markdown file per ticket under `.scratch/<feature>/` | v1.3.2 / `engineering/to-tickets` (patched) |
| [implement](./skills/engineering/implement/SKILL.md) | Implements against a spec or a single ticket, calling `tdd` at agreed seams and `code-review` before committing | v1.3.2 / `engineering/implement` (patched) |
| [implement-spec](./skills/engineering/implement-spec/SKILL.md) | Implements a whole spec on a single integration branch, driving tickets as a task graph | v1.3.2 / `engineering/implement-spec` (patched) |
| [retro](./skills/engineering/retro/SKILL.md) | Session retrospective: ranks improvements to the coding agent environment (navigation, automated checks, standards, steering files, toolchain) by severity | v1.3.2 / `engineering/retro` (as-is) |
| [project-preset-for-skills](./skills/engineering/project-preset-for-skills/SKILL.md) | One-time setup before first use: writes the domain doc layout under `docs/agents/` | v1.3.2 / `engineering/setup-matt-pocock-skills` (renamed, patched) |
| [redesign-existing-projects](./skills/engineering/redesign-existing-projects/SKILL.md) | Lifts an existing site or app to a premium feel: audits the current state, spots generic AI styling, applies high-end visual standards without breaking behaviour | taste-skill v2.1.0 / `skills/redesign-skill` (patched) |

Model-invoked:

| Skill | Purpose | Source |
| --- | --- | --- |
| [prototype](./skills/engineering/prototype/SKILL.md) | Throwaway prototype: a single HTML file to test a state model and its logic, or switchable UI variants to test an interface | v1.3.2 / `engineering/prototype` (as-is) |
| [diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md) | Diagnosis loop for hard bugs and performance regressions: build a feedback loop that can fail, then minimise, hypothesise, instrument, fix and add a regression test | v1.3.2 / `engineering/diagnosing-bugs` (as-is) |
| [research](./skills/engineering/research/SKILL.md) | A background agent reads primary sources and settles findings into a cited Markdown file | v1.3.2 / `engineering/research` (as-is) |
| [tdd](./skills/engineering/tdd/SKILL.md) | Red, green, refactor loop, delivered one vertical slice at a time | v1.3.2 / `engineering/tdd` (as-is) |
| [domain-modeling](./skills/engineering/domain-modeling/SKILL.md) | Actively builds and sharpens a domain model: challenges terms, stress-tests with scenarios, keeps `GLOSSARY.md` and ADRs in step | v1.3.2 / `engineering/domain-modeling` (as-is) |
| [codebase-design](./skills/engineering/codebase-design/SKILL.md) | Shared vocabulary for deep module design: small interfaces, clean seams, testable through the interface | v1.3.2 / `engineering/codebase-design` (as-is) |
| [code-review](./skills/engineering/code-review/SKILL.md) | Two-axis review: Standards (repo conventions, common smells) and Spec (fidelity to the original spec), run as parallel sub-agents | v1.3.2 / `engineering/code-review` (patched) |

### Productivity (7)

User-invoked:

| Skill | Purpose | Source |
| --- | --- | --- |
| [grill-me](./skills/productivity/grill-me/SKILL.md) | Stateless continuous questioning, for cases with no working directory to write into | v1.3.2 / `productivity/grill-me` (as-is) |
| [handoff](./skills/productivity/handoff/SKILL.md) | Compresses the current conversation into a handoff document for another agent to pick up | v1.3.2 / `productivity/handoff` (as-is) |
| [teach](./skills/productivity/teach/SKILL.md) | Treats the current directory as a stateful teaching space, spreading one concept or skill across sessions | v1.3.2 / `productivity/teach` (as-is) |
| [wait-what](./skills/productivity/wait-what/SKILL.md) | Correction prompt for a message you did not follow: makes the agent re-explain in terms you already have and supply the missing context | v1.3.2 / `productivity/wait-what` (as-is) |

Model-invoked:

| Skill | Purpose | Source |
| --- | --- | --- |
| [find-skills](./skills/productivity/find-skills/SKILL.md) | Searches the public skills ecosystem for an installable skill, vets it by install count and source reputation, then offers the install command | `57217cf` / `skills/find-skills` (patched) |
| [grilling](./skills/productivity/grilling/SKILL.md) | The questioning primitive itself: advances the design tree round by round, facts to the agent, decisions to you | v1.3.2 / `productivity/grilling` (as-is) |
| [writing-for-agents](./skills/productivity/writing-for-agents/SKILL.md) | Docs whose reader is not a human: skills, `AGENTS.md` / `CLAUDE.md`, anything reached through a pointer | v1.3.2 / `productivity/writing-for-agents` (as-is) |

## Usage

### Invocation model

The boundary between the two kinds is defined in [.agents/invocation.md](./.agents/invocation.md):

- **User-invoked**: the `SKILL.md` frontmatter carries `disable-model-invocation: true`, and `agents/openai.yaml` carries `policy.allow_implicit_invocation: false`. Only a human typing `/skill-name` can trigger them, and other skills cannot reach them through the Skill tool either. The `description` is written for humans: one sentence on what it does.
- **Model-invoked**: neither field is present, so the model triggers them at its own judgement. The `description` is written for the model and keeps the "use this when" triggers.

One hard rule: a user-invoked skill may call model-invoked skills, never the reverse. Calls from `implement` and `implement-spec` into `tdd` and `code-review` are therefore legal, while any skill needing `project-preset-for-skills` can only phrase it as an instruction for a human to carry out.

### Installing locally

Pick either option:

1. **Local symlinks**

   ```bash
   bash scripts/link-skills.sh
   ```

   The script symlinks every skill directory under `skills/` into `~/.claude/skills` and `~/.agents/skills`, so a `git pull` takes effect immediately. **Caveat**: if a real directory (not a symlink) of the same name already exists at the target, the script runs `rm -rf` on it before creating the link. Check that the target holds no uncommitted local changes first.

2. **Manual copy**

   Copy the skill directory into the skills directory of whichever harness you use. `SKILL.md` and `agents/` must stay siblings.

### Typical workflow

```text
project-preset-for-skills (once per repo)
        │
        ▼
grill-with-docs ──► to-spec ──► to-tickets ──► implement (or implement-spec for concurrent work)
        │                                      │
        │                                      ├──► tdd (implement one slice)
        │                                      └──► code-review (two-axis review before commit)
        ▼
   GLOSSARY.md / ADR                           retro (environment improvements after the session)
```

Side paths and supplements: `prototype` turns design questions that paper cannot settle into a throwaway program; `research` hands verification to a background agent; `diagnosing-bugs` handles problems that resist reproduction; `grill-me` and `grilling` are questioning entry points that need no files on disk; `redesign-existing-projects` stands alone for visual overhauls of existing projects; `find-skills` looks outside this repo, searching the public skills ecosystem when nothing here covers the capability.

When unsure which skill to use, run `ask-help` first. It is the routing table for this flow.

## Maintenance

### Adding a skill

Under the rules in [AGENTS.md](./AGENTS.md), `engineering/` and `productivity/` are the promoted buckets, and adding a skill means updating 7 places. Miss one and the docs no longer match the implementation:

1. `skills/<bucket>/<name>/SKILL.md`: frontmatter with at least `name` and `description`; add `disable-model-invocation: true` for user-invoked skills.
2. `skills/<bucket>/<name>/agents/openai.yaml`: `interface.display_name` and `interface.short_description`; add `policy.allow_implicit_invocation: false` for user-invoked skills.
3. The bucket `README.md`: file the skill under User-invoked or Model-invoked, with its name linked to `SKILL.md`.
4. The matching tables in both `README.md` and `README.zh-CN.md`: both need the row, and the descriptions must agree.
5. The `skills` array in `.claude-plugin/plugin.json`.
6. If the skill sits on a user-reachable path, reread [ask-help](./skills/engineering/ask-help/SKILL.md) and update its routing. A missing or stale entry leads to wrong advice.
7. The source table in [NOTICE.md](./NOTICE.md); if the content departs from the upstream file, add a patch under `patches/`.

### Renaming or deleting

A rename touches the directory name, the `name` in `SKILL.md`, `display_name` in `agents/openai.yaml`, both bucket READMEs, both top-level READMEs, `plugin.json`, the upstream path mapping in `NOTICE.md`, and the patch filenames under `patches/`. Patch filenames keep the upstream path and do not follow the rename.

A delete cleans up the same places in reverse and drops the matching patch from `patches/`.

### Versioning and changelog

```bash
npm run changeset              # write a change description
npm run version                # run changeset version, then sync the plugin.json version
npm run check-plugin-version   # only check that package.json and plugin.json agree
```

`package.json` is the single source of truth for the version; `scripts/sync-plugin-version.mjs` writes it into `plugin.json`. Do not edit both files by hand. Both currently read `1.0.0`.

### Documentation consistency check

```bash
# Full skill inventory, straight from the files
bash scripts/list-skills.sh

# Diff skill directories on disk against the plugin.json skills array:
# left column is disk-only, right column is manifest-only
comm -3 \
  <(find skills -name SKILL.md | sed 's|/SKILL.md$||; s|^|./|' | sort) \
  <(python -c "import json;print('\n'.join(sorted(json.load(open('.claude-plugin/plugin.json'))['skills'])))" | tr -d '\r')

# Compare the heading levels of the two READMEs to catch structural drift.
# Fenced blocks are skipped so shell comments are not counted as headings.
diff \
  <(awk '/^```/{f=!f;next} !f&&/^#/{match($0,/^#+/);print RLENGTH}' README.md | sort | uniq -c) \
  <(awk '/^```/{f=!f;next} !f&&/^#/{match($0,/^#+/);print RLENGTH}' README.zh-CN.md | sort | uniq -c)
```

When the first two commands print nothing, the manifest and the implementation agree. The third compares how many headings sit at each level, which is language independent: identical output means the two files still have the same shape.

### Upstream sync

Read [patches/README.md](./patches/README.md) before syncing with upstream. The procedure: clone the target tag with an LF checkout, apply the existing patches in order, then redo the diff. Patches must be generated with LF line endings and applied with `git -c core.autocrlf=false apply`. Windows defaults to `core.autocrlf=true`, which writes the result as CRLF and makes the byte-level check fail every time.

## License

Released under the MIT licence, see [LICENSE](./LICENSE). All three upstream repositories are MIT as well; sources, paths and commits are in [NOTICE.md](./NOTICE.md).
