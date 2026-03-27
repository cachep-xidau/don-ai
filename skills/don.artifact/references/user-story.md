# User Story

Write one lean user story for one behavior slice.

Use this reference for behavior and business value only.

- Exact UI text, field inventory, and button inventory belong in `screen-description.md`
- NFR detail belongs in `function-list.md`
- SQL, validation logic, API detail, and payload constraints belong in `srs.md`

## Markdown Format

- `# User Stories: [Module/Feature]` — Container title when output is aggregated
- `## US-XXX-NNN: [Story Title]` — One story entry
- `### Section` — Story-local sections such as References, Acceptance Criteria, Business Rules
- `#### AC-N: Name` — One acceptance criterion under the current story

> **UI text capture** belongs in Screen Description, not User Story. See [`screen-description.md`](screen-description.md).

## Output Contract

- Default Don output: append each story under `artifact/user-stories.md`
- Story identifier format: `US-[MODULE]-[NUMBER]`
- If the user explicitly wants one standalone file per story, follow the user's naming rule or project convention. Do not silently invent a second output structure.
- If standalone output is requested without a naming rule, follow the active project or workspace document naming convention.

## Template

```markdown
## US-XXX-NNN: [Short descriptive title]

### References

| Type | Link |
|------|------|
| Figma | [URL] |
| Function List | [FL-XXX-NNN] |
| SRS | [SRS-XXX-NNN] |
| Related US | [US-XXX-NNN] |

### User Story

**As a** [role]
**I want** [action]
**So that** [benefit]

### Pre-conditions

- [condition 1]
- [condition 2]

### Entry Point

[Screen Name] > [Section] > [Action]

### Acceptance Criteria

#### AC-1: [AC Name]

[Context], user [action], system [expected result]

#### AC-2: [AC Name]

[Context], user [action], system [expected result]

### Business Rules

- **BR-001:** [Rule description]
- **BR-002:** [Rule description]

### Exception Handling

- **[Exception scenario]:** [System response]
- **[Exception scenario]:** [System response]
```

## Acceptance Criteria Format

Use pattern: `User [action] → System: [response]`

**Example:**
```markdown
#### AC-1: Save Widget Preferences

User taps Save button → System:
- Validates minimum 1 widget enabled [Ref: SRS-TOD-010-V1]
- Persists preferences to database
- Displays success toast
- Provides haptic feedback
```

**Guidelines:**
- Focus on observable behavior (not implementation)
- Use bullet list for multi-step responses
- Never embed code - describe behavior only

## Writing Rules

- Keep the story independent and sprint-sized
- Use one primary actor and one clear goal
- Keep Acceptance Criteria testable and observable
- Keep Business Rules short and policy-like
- If context is missing, separate assumption from fact instead of filling the gap silently

## Code References

User stories describe **WHAT** (behavior), not **HOW** (code).

**Never embed code blocks** - SQL, JavaScript, JSON belong in SRS documents.

**When referencing implementation:** `[Ref: DOC-TYPE-MODULE-ITEM]`

Examples:
- `[Ref: SRS-TOD-010-V1]` - validation logic
- `[Ref: SRS-TOD-010-Q1]` - SQL query
- `[Ref: FL-XXX-YYY]` - function spec

Keep all code-prohibition guidance in this reference and move executable detail into SRS references instead of helper docs.

## Code Migration Checklist

**Prohibited in User Stories:**
- ❌ SQL queries
- ❌ JavaScript/TypeScript validation logic
- ❌ JSON configuration objects
- ❌ API request/response payloads
- ❌ Regular expressions
- ❌ Algorithm pseudocode

**Migration Steps:**
1. Extract code from user story AC
2. Create/update SRS with reference IDs (e.g., `[Ref: SRS-TOD-010-Q1]`)
3. Replace code blocks with behavior descriptions + reference notation
4. Add SRS link to References section
5. Verify user story focuses on observable behavior only

## INVEST Criteria

- **I**ndependent - No dependencies on other stories
- **N**egotiable - Details can be discussed
- **V**aluable - Provides user/business value
- **E**stimable - Can be sized
- **S**mall - Fits in a sprint
- **T**estable - Has pass/fail criteria

## Visual Properties (EXCLUDED)

User stories focus on **behavior and value**, not visual implementation.

**Never include:**
- **Colors:** No hex codes, RGB, design tokens (e.g., "primary-500")
- **Typography:** No fonts, sizes, weights (e.g., "Inter 16px bold")
- **Spacing:** No padding, margin, gap (e.g., "16px padding")
- **Effects:** No shadows, borders, curves, radius (e.g., "8px border radius")
- **Layout:** No positioning, alignment specs (e.g., "centered", "fixed top")

> Visual specs = Figma only. User stories describe WHAT user achieves, not HOW it looks.
>
> If a sentence depends on color, spacing, typography, radius, shadow, position, or animation tokens, remove it from the user story and capture it in Figma or Screen Description instead.

## What NOT to Include

User stories focus on **WHAT** user achieves, not implementation details.

**Exclude from user stories:**
- Metadata tags or duplicate identifiers outside the story heading/ID
- Post-conditions (implied by AC completion)
- NFRs - performance/security specs (use Function List)
- UX/UI specifications (use Figma, Screen Description)
- Visual properties - color, radius, spacing, typography (use Figma)
- Dependencies (use project roadmap)
- Testing scenarios (use QA test plans)

**Remember:** Describe user value and observable behavior only.

## Cross-Reference Rule

If implementation detail must be referenced, point to the owning artifact instead of embedding it inline.

Examples:
- Validation rule -> `[Ref: SRS-TOD-010-V1]`
- Query or persistence behavior -> `[Ref: SRS-TOD-010-Q1]`
- Function scope -> `[Ref: FL-TOD-010]`

## Self-Review Checklist

Trước khi output, verify:

- [ ] Có đủ actor, action, và benefit trong narrative
- [ ] Story ID đúng format `US-XXX-NNN`
- [ ] Output structure phù hợp contract hiện tại: aggregate by default, standalone only if explicitly requested
- [ ] Nếu standalone file được yêu cầu, filename follow user rule hoặc project/workspace convention
- [ ] Heading depth đúng với output mode hiện tại, không flatten structure khi story được aggregate
- [ ] Có ít nhất 1 Acceptance Criteria và mỗi AC mô tả behavior có thể test được
- [ ] INVEST: Independent, Negotiable, Valuable, Estimable, Small, Testable
- [ ] AC dùng active voice, single thought per sentence
- [ ] Không có vague terms: "some", "many", "appropriate", "sufficient", "flexible"
- [ ] Không có code block (SQL, JS, JSON) → dùng `[Ref: SRS-...]`
- [ ] Không có visual specs (color, spacing, typography) → Figma only

**Phát hiện vi phạm → tự sửa trước khi output.**
