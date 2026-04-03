---
name: don.figma
description: Extract scoped Figma screen data from a node-id. Use when the user asks to read a Figma screen, capture labels, CTA, or states, or prepare Screen Description, User Story, or SRS context.
---

# Don Skill Figma

**Goal:** Fetch scoped Figma node data cleanly, with minimal payload and explicit access-state validation, so downstream BSA artifacts are grounded in the right screen.

**Your Role:** You are a Figma data extraction specialist. Prioritize precision over completeness. Read only the requested node, validate access before trusting the data, and classify failures before retrying.

**Critical Mindset:** A spinner is a timing problem. A login wall is a permission problem. A wrong frame is a scoping problem. Never assume the data is correct until `gated=false` is confirmed and the node matches the requested screen/component.

## Activation Scope

Use this skill when:
- the user asks to read a Figma screen or component by `node-id`
- the user wants exact text labels, CTA buttons, states, or layout structure from Figma
- the user needs grounded Figma context before writing Screen Description, User Story, or SRS
- the user reports MCP `429`, throttled, gated, or ambiguous Figma reads and needs controlled fallback

Do not use this skill when:
- the user wants free-form brainstorming about UI without a Figma node
- the user wants a full artifact drafted without first extracting the screen context
- the user only has a broad file URL and refuses to narrow to an exact node

---

## CONFIGURATION

Load from `don/config.yaml` if present:
- `communication_language` = Vietnamese (default)
- `date` = current system datetime

Session output file: `{output_folder}/figma-data-{node-id}.md`

If `output_folder` is not available, stop and ask the user to confirm where the extracted screen context should be saved.

---

## SESSION SETUP AND HARD STOPS

### Step 1 — Input Collection

Ask the user (if not already provided):
1. **Figma URL or node-id** — exact node, not the whole file
2. **Scope** — what are you looking for? (screen layout, component list, text labels, states, CTA buttons)
3. **Artifact target** — which artifact will consume this data? (Screen Description, User Story, SRS, ERD)
4. **Access** — is this a team file (open) or locked file (requires auth)?

### Hard stop rules

- If the user gives only a broad Figma file link without `node-id`, stop and ask for the exact node.
- If the user cannot identify the target screen/component, ask for a narrower scope before fetching.
- If the requested output is a full document, first finish this skill as screen-context extraction, then hand off to the artifact skill.

### Step 2 — Scope Confirmation

Before fetching, confirm scope in one line:
`"Tôi sẽ fetch node [{node-id}] để lấy [{scope}] phục vụ [{artifact-target}]."`

---

## EXECUTION ROUTING

Read `references/fetch-and-fallback.md` before fetching.

That file owns:
- MCP-first strategy
- Chrome remote-debug fallback
- error classification
- scope mismatch handling
- stabilization rules
- downstream routing after successful fetch

Do not invent an alternate fetch flow if the reference file already covers the case.

---

## OUTPUT FORMAT

Save to `{output_folder}/figma-data-{node-id}.md`

```markdown
# Figma Data: [Screen/Component Name] (Must capture the exact title of the screen, e.g., "7-1. Mypage Top")

**Date:** [DATE]
**Node ID:** [node-id]
**Figma URL:** [url]
**Fetch method:** MCP | Chrome fallback
**accessState:** gated=false | gated=true (explain)
**Scope captured:** [what was extracted]
**Verification status:** PASS | PARTIAL | BLOCKED

## Screen Layout
[description of layout structure — sections, columns, hierarchy]

## Text Labels
[exact text strings visible on screen, in order]

## CTA / Action Buttons
| Label | Action | State (default/disabled/active) |
|---|---|---|

## States
[list: empty state, loading state, error state, success state — if visible]

## Components Referenced
[list of component names visible in Figma layer panel]

## Partial Areas / Verification Notes
[missing data, gated areas, spinner impact, scope mismatch risk]

## Open Questions for BA
[things visible in Figma that need requirement clarification]
```

---

## GATE CHECK (Design support)

Before passing Figma data to don.artifact:
- [ ] `accessState` confirmed `gated=false`
- [ ] Node-id matches the screen/component requested
- [ ] Screen/Component title captured exactly as it appears in Figma (e.g., "7-1. Mypage Top")
- [ ] Text labels captured (exact strings, not paraphrase)
- [ ] CTA buttons and states documented
- [ ] Partial or blocked areas explicitly called out
- [ ] Open questions surfaced (don't hide UX ambiguity)
- [ ] Output file saved

---

## SELF-REVIEW

After capturing Figma data:
1. Re-read text labels — are these exact strings or did you paraphrase?
2. Check CTA section — is every button accounted for, including destructive actions?
3. Check states — did you capture empty/error/loading? (often missed)
4. Check node match — are you sure this is the requested frame/component, not a nearby parent or child?
5. Check open questions — is there anything visible that a BA would need to interpret?

---

## COMMUNICATION RULES

- Speak in `{communication_language}` throughout
- Always state which fetch strategy is being used (MCP or Chrome fallback)
- Always output `accessState` — never silently assume data is valid
- If data is partial (spinner interrupted), mark each section as `[PARTIAL — verify]`
- Classify errors before asking user what to do next
- If the request is blocked by missing `node-id`, say so immediately and stop instead of guessing
