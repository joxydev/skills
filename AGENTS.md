# Working on this repo (for agents and humans)

This repo is a library of **106 social media skills** (`skills/`) plus **tool integration
guides** (`tools/integrations/` + `tools/REGISTRY.md`). Skills follow the
[Agent Skills](https://agentskills.io) convention: a directory with `SKILL.md`
(frontmatter `name` matching the directory + a long routing `description`), `references/`
deep-dives, and `evals/evals.json`.

## Before every task: skill discovery and use

- Review the available skill catalog, including skills supplied by the runtime and plugins.
  This repository's skills are also discoverable under `.agents/skills/` and live in
  `skills/`. For this large library, use `SKILLS-CATALOG.md` as a searchable index and
  inspect current skill directories as needed; the runtime's injected list can be
  truncated and the index is a snapshot. Do not assume the index contains plugins or
  runtime skills from another session.
- Identify the skills relevant to the request from their names and descriptions. When the
  user explicitly names a skill, include it in the plan; avoid selecting skills solely on
  superficial keyword matches.
- Read the complete `SKILL.md` of each selected skill through its available provider, then
  follow its applicable instructions and load referenced resources when required. User
  instructions and higher-priority instructions take precedence over skill guidance.
- Do not silently ignore a relevant skill. If a selected skill cannot be loaded, report why
  and proceed as far as possible. If no skill is relevant, proceed normally.
- A skill's presence does not guarantee its external tools, services, credentials, or
  dependencies are available. Check the capabilities needed for the actual task.

## Product content: verstakmd

Before preparing content, editing product imagery, or planning publications for the shop,
read `brand/brand-profile.md`, `brand/visual-style-guide.md`, and `brand/product-rules.md`,
then apply `docs/agent-operating-rules.md` and the relevant task-specific templates.
Treat the brand profile as provisional where it requests confirmation. Use real product
photos as the reference for the product's actual appearance. Full image generation from
the supplied photograph is allowed: repeat all visible details, wood texture, grain,
color, carving, lettering, faces, hands, and proportions as accurately as possible while
changing the requested composition, background, table, and placement. An original pixel
layer or editing mask is not required. Follow the product-preservation rules and inspect
the generated result against the reference rather than promising pixel identity.
Do not invent product facts, customer proof, prices, or delivery terms. Ask only for
information needed to complete the current task and provide two or three options when
appropriate. Obtain the required confirmation before scheduling or publishing.
For relevant marketing strategy, social, copywriting, or advertising tasks, also inspect
the applicable skill in `vendor/marketing-skills/skills/`; these are pinned local copies
and are not automatically listed as Codex-discoverable skills. Read the full relevant
`SKILL.md` and necessary resources, subject to the user's instructions and project rules.

## Before committing anything

```bash
./scripts/validate-skills.sh
```

It checks structure, frontmatter, evals JSON, cross-reference resolution, pack integrity, and
banned claim patterns. CI runs the same script on every PR.

## Ground truths (do not contradict these anywhere)

- Skills route publishing through a **scheduling bridge**; its canonical capability surface
  lives in [tools/integrations/woopsocial.md](tools/integrations/woopsocial.md) — treat that
  guide as the source of truth and never restate its specifics (platform list, limits, caps)
  from memory.
- The bridge **publishes and schedules**, and it stores **lifetime post analytics** for
  TikTok, LinkedIn, Facebook, Instagram, Pinterest, YouTube, and Bluesky. It does not generate
  or edit media. House phrasing wherever measurement comes up: read WoopSocial post analytics
  for those networks; use the native dashboard for X, Threads, Reddit, and for any metric
  WoopSocial doesn't store. Never fabricate a number.
- One content item per post; changing a scheduled post = delete + recreate, confirmed.
- **Nothing is scheduled, published, or deleted without explicit user confirmation.**
- The validator (`scripts/validate-skills.sh`) enforces the common violations mechanically.

## House style for skills

- One skill = one job-to-be-done; explicit sibling routing in the description (the trigger
  surface); every backticked `skill-name` must resolve to a real `skills/` directory.
- Opinionated, anti-hype, current: teach how top practitioners do the job now. Never fabricate
  stats; attribute volatile figures with a **verify-quarterly** tag. No engagement-bait.
- Reference-file pattern: `scope-and-connections.md`, a `<topic>-2026-reality.md`, a named
  framework file, a recipes/templates file.

## Build tooling

- `scripts/build-skill-zips.sh` — one self-contained ZIP per skill into `dist/` (embeds each
  skill's referenced tool guides under `references/tools/`).
- `scripts/build-packs.sh` — topic-pack bundles into `dist/packs/` from `scripts/packs.json`.
- `dist/` is generated and gitignored; rebuild before each release and attach to it.

## Releases

Bump `version` in `.claude-plugin/plugin.json` **and** `.claude-plugin/marketplace.json`, add a
`VERSIONS.md` entry, tag, and attach fresh `dist/` ZIPs to the GitHub release.

For verstakmd product imagery, read `skills/verstak-product-reference/SKILL.md` and its reference inventory. Icons stand upright on the table; backgammon and chess boards lie flat.
