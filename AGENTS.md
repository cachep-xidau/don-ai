# AGENTS.md

This repository is a small public share pack.

## Repo Purpose

The repo contains:
- `AGENTS.md`
- `README.md`
- `skills/don.figma/`
- `skills/don.artifact/`

The core share payload is:
- `skills/don.figma/`
- `skills/don.artifact/`

It is not the full Don package.
It does not include the orchestrator, phase-gate workflows, command surface, or internal workspace rules.

## Read Order

Before changing anything, read in this order:
1. `README.md`
2. the target skill's `SKILL.md`
3. the target skill's `references/*`

`SKILL.md` is the source of truth for skill behavior.
`README.md` is quick-start only.

## Boundaries

- Do not assume any private workspace structure.
- Do not assume local absolute paths.
- Do not assume hidden external rule files, MCP servers, or internal deployment context.
- Do not widen this repo into a template for unrelated projects.
- Do not copy a skill directory without its `references/` folder.

## Usage Rules

### `don.figma`

Use it when the consumer needs scoped Figma extraction from an exact `node-id`.

Rules:
- require an exact `node-id`
- keep fetch scope narrow
- do not paraphrase visible labels or CTA text
- mark partial or blocked data explicitly

### `don.artifact`

Use it when the consumer needs exactly one artifact drafted.

Supported artifacts:
- Screen Description
- User Story
- Technical Story
- Function List
- SRS
- ERD
- Use Case Diagram
- Sequence Diagram

Rules:
- one artifact per run
- do not silently widen a request into a package
- technical artifacts are explicit-only
- weak context stays weak; do not invent facts

## Sync Rules

When updating this repo:
- sync `SKILL.md` and `references/*` together
- keep README aligned with actual repo contents
- review diffs before push
- keep the package narrow

## Contribution Rule

Prefer minimal, repo-specific instructions.
If a rule only makes sense in a private workspace, it does not belong here.
