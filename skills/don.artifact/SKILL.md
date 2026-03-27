---
name: don.artifact
description: Writes one Don design artifact at a time. Use when the user asks to draft a Screen Description, User Story, Technical Story, Function List, SRS, ERD, Use Case, or Sequence diagram.
argument-hint: "[artifact-type] [requirements-context]"
allowed-tools: Bash, Read, Glob, Grep
---

# Don Artifact Skill

Produce one bounded artifact at a time from confirmed requirements. Keep the scope explicit, load only the local reference that owns the requested artifact type, and do not expand a vague design ask into a package by default.

## Scope

Use this skill when the user explicitly asks for:
- Screen Description
- User Story
- Technical Story
- Function List
- SRS
- ERD
- Use Case diagram
- Sequence diagram

Do not use this skill when:
- the user wants requirements analysis, gap analysis, or stakeholder framing
- the user asks for multiple artifact types without naming them
- the source context is too weak to choose a single artifact safely
- the user really needs scoped Figma extraction before any artifact can be drafted

## Routing Contract

Read [`references/artifact-routing.md`](./references/artifact-routing.md) before drafting.

That file owns:
- artifact selection
- explicit-only technical artifact rule
- self-review routing
- boundary with requirements analysis
- boundary with scoped Figma extraction

## Workflow

1. Confirm artifact type and requirements context.
2. Load exactly one matching reference file.
3. Draft the artifact from that reference only.
4. Reload the same reference and run its self-review checklist.
5. Fix violations before output.
6. If the user asked vaguely for "design docs" or "solution docs", stop and force artifact selection instead of choosing a package silently.

## Artifact Map

| Artifact | Reference |
|---|---|
| Screen Description | `references/screen-description.md` |
| User Story | `references/user-story.md` |
| Technical Story | `references/technical-story.md` |
| Function List | `references/function-list.md` |
| SRS | `references/srs.md` |
| ERD | `references/erd-dbdiagram.md` |
| Use Case | `references/use-case-diagram.md` |
| Sequence | `references/sequence-diagram.md` |

## Guardrails

- Keep business artifacts lean and behavior-focused.
- Do not generate Technical Story unless the user explicitly asks for `Technical Story` or `Enabler Story`.
- Do not generate ERD, Use Case, or Sequence unless explicitly requested.
- Do not widen a single-artifact request into a multi-artifact package.
- Do not collapse weak context into facts.
- Route requirements analysis asks to `don.analysis`.
- Route scoped Figma extraction asks to `don.figma`.
- Preserve the local reference structure and self-review rules.
