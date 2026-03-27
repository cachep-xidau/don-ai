# Artifact Routing

Use this file after artifact type and context are confirmed.

## Artifact Routing Table

| Artifact | Reference | Notes |
|---|---|---|
| Screen Description | `references/screen-description.md` | Default business artifact for screen-level context |
| User Story | `references/user-story.md` | Lean format, actor-driven, AC-focused |
| Technical Story | `references/technical-story.md` | Explicit-only enabler / architecture / infrastructure / compliance story |
| Function List | `references/function-list.md` | Main Flow + NFR only |
| SRS | `references/srs.md` | Business + system requirement structure |
| ERD | `references/erd-dbdiagram.md` | Explicit-only technical artifact |
| Use Case | `references/use-case-diagram.md` | Explicit-only technical artifact |
| Sequence | `references/sequence-diagram.md` | Explicit-only technical artifact |

## Explicit-Only Technical Artifacts

The following must not be generated unless the user requests them by name:

- `Technical Story`
- `Enabler Story`
- `ERD`
- `DBML`
- `Use Case`
- `Sequence Diagram`
- `ARCH`

If the user asks generally for “design docs” or “solution docs”, default to business-safe artifacts first and ask which artifact they actually want.

## Self-Review Routing

After drafting, reload the matching reference and run its self-review section if present.

- User Story → `references/user-story.md`
- Technical Story → `references/technical-story.md`
- Screen Description → `references/screen-description.md`
- Function List → `references/function-list.md`
- SRS → `references/srs.md`
- ERD → `references/erd-dbdiagram.md`
- Use Case → `references/use-case-diagram.md`
- Sequence → `references/sequence-diagram.md`

Fix violations before final output.

## Boundaries With Other Skills

Use `don.analysis` instead when the user really needs:

- FR/NFR analysis
- gap-impact analysis
- stakeholder analysis
- requirement normalization notes

Use `don.figma` instead when the user needs:

- scoped Figma fetch
- node-id extraction
- compact screen context from Figma

NFR details belong in `Function List`, not `User Stories`, unless the source context explicitly says otherwise.

Use `Technical Story` when the user explicitly needs:

- enabler work made visible as a bounded story
- architecture / infrastructure / compliance work with acceptance evidence
- technical risk reduction tied to downstream delivery

Do not use `Technical Story` as a hiding place for vague tasks, generic refactors, or unfunded architecture dreams.

## Non-Negotiable Rules

- Do not output a default multi-artifact package unless the user explicitly names the members.
- Do not draft technical diagrams from weak or missing system context.
- Do not collapse assumptions into facts.
- Do not silently widen scope from one artifact into many.
