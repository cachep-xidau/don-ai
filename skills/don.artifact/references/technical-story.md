# Technical Story

Write one bounded technical story for one enablement slice.

Use this reference only when the user explicitly asks for:
- `Technical Story`
- `Enabler Story`
- a developer-facing architecture / infrastructure / compliance / exploration story

This artifact is not a replacement for User Story. It exists to make technical enablement visible without collapsing it into vague tasks or hidden backlog debt.

## What a Technical Story Is

A technical story is a small, acceptance-driven technical slice that:
- enables future business stories
- reduces concrete delivery risk
- improves architecture, infrastructure, compliance, or technical quality
- can be completed and verified within one iteration or one bounded delivery slice

Use SAFe-style enabler semantics:
- **Exploration** - prove feasibility, compare options, de-risk unknowns
- **Architecture** - establish or change structural system capability
- **Infrastructure** - create platform or delivery foundations
- **Compliance** - satisfy audit, security, or regulatory constraints

## What a Technical Story Is Not

Do not use this artifact for:
- raw task lists
- vague refactor placeholders
- "upgrade X" with no risk, outcome, or acceptance evidence
- architecture redesign proposals with no bounded delivery slice
- user-visible behavior stories that should stay in `user-story.md`

If the ask is user-facing and actor-benefit oriented, route back to `user-story.md`.

## Markdown Format

- `# Technical Stories: [Module/Feature]` - Container title when output is aggregated
- `## TS-XXX-NNN: [Story Title]` - One technical story entry
- `### Section` - Story-local sections such as References, Acceptance Criteria, Risks
- `#### AC-N: Name` - One acceptance criterion under the current story

## Output Contract

- Default Don output: append each story under `artifact/technical-stories.md`
- Story identifier format: `TS-[MODULE]-[NUMBER]`
- If the user explicitly wants one standalone file per story, follow the user's naming rule or project convention
- If standalone output is requested without a naming rule, follow the active project or workspace document naming convention

## Standard Position

There is no single universal cross-industry template for "technical story."

Don adopts a conservative standard inferred from:
- classic user story quality rules: small, testable, traceable, acceptance-driven
- Agile guidance: do not confuse stories with component/task breakdown
- SAFe guidance: enabler stories cover exploration, architecture, infrastructure, and compliance work

Therefore this reference requires:
- one bounded technical objective
- explicit technical value or risk reduction
- traceability to business or solution artifacts
- observable acceptance evidence

## Template

```markdown
## TS-XXX-NNN: [Short technical outcome title]

### Classification

- **Type:** Exploration | Architecture | Infrastructure | Compliance
- **Driver:** Performance | Security | Reliability | Maintainability | Delivery | Compliance
- **Priority:** Must | Should | Could

### References

| Type | Link |
|------|------|
| PRD | [prd.md section or ID] |
| Architecture | [architecture.md section or ID] |
| Function List | [FL-XXX-NNN] |
| SRS | [SRS-XXX-NNN] |
| Related US | [US-XXX-NNN] |
| Related TS | [TS-XXX-NNN] |

### Technical Story

**In order to** [technical capability or risk reduction]
**The team needs** [bounded technical change]
**So that** [user story, delivery, quality, or compliance outcome]

### Problem Statement

[Current technical gap, risk, or constraint in 2-4 lines]

### Scope

- **In scope:** [bounded item]
- **In scope:** [bounded item]
- **Out of scope:** [excluded item]

### Pre-conditions

- [condition 1]
- [condition 2]

### Acceptance Criteria

#### AC-1: [Observable technical outcome]

Given [initial technical state], when [change or validation occurs], then:
- [observable result]
- [evidence or proof expected]

#### AC-2: [Risk or quality gate]

Given [condition], when [check is executed], then:
- [technical outcome]
- [proof artifact]

### Evidence

- **Test/Check:** [test suite, smoke check, migration check, static check]
- **Metric/Signal:** [latency, error rate, coverage, audit proof, build proof]
- **Artifact:** [ADR, migration file, config file, runbook, dashboard]

### Risks

- **Risk:** [main risk]
- **Mitigation:** [how risk is contained]

### Follow-up

- [next dependent user story or technical story]
```

## Writing Rules

- Keep it sprint-sized and acceptance-driven
- State technical value explicitly: risk reduction, capability enablement, compliance proof, or delivery acceleration
- Use one primary technical outcome only
- Keep scope bounded enough that a team can finish it without hidden sub-projects
- Tie it to downstream business value or solution continuity
- Separate confirmed fact, assumption, and open question
- Prefer observable outcomes over implementation narration

## Acceptance Criteria Rules

Acceptance Criteria must prove technical completion, not just effort spent.

Good evidence:
- migration runs successfully and rollback path exists
- new gateway path passes smoke + auth checks
- build pipeline enforces the new rule
- audit artifact generated and reviewable
- performance threshold or error budget is met

Bad evidence:
- developer updated code
- refactor completed
- framework upgraded
- cleanup done

Use one of these patterns:

1. `Given [technical context], when [check/event], then [observable system result]`
2. `System must provide [technical capability] with [measurable constraint]`
3. `Required evidence exists in [artifact/test/check] and proves [outcome]`

## INVEST Interpretation For Technical Stories

- **Independent** - can be delivered without bundling multiple unrelated technical changes
- **Negotiable** - solution detail can change while intent stays stable
- **Valuable** - value may be indirect, but must be explicit
- **Estimable** - team can size it without hidden discovery swamp
- **Small** - fits one iteration or one bounded slice
- **Testable** - clear proof exists for done / not done

## Cross-Reference Rule

If detailed implementation must be referenced, point to the owning artifact instead of embedding it inline.

Examples:
- validation logic -> `[Ref: SRS-XXX-NNN-V1]`
- SQL or migration query -> `[Ref: SRS-XXX-NNN-Q1]`
- API change -> `[Ref: SRS-XXX-NNN-API-01]`
- business dependency -> `[Ref: US-XXX-NNN]`

## What NOT to Include

Exclude from technical stories:
- raw engineering task checklist
- full code blocks
- stack dump or investigation log with no recommendation
- UI copy or visual specs
- generic statements like "improve maintainability" without proof
- multi-epic architecture roadmaps
- low-level file-by-file task decomposition

Technical stories describe the bounded **why + what + proof**, not the entire implementation plan.

## Good Example

```markdown
## TS-AUTH-014: Enforce Token Rotation in Background Workers

### Classification

- **Type:** Infrastructure
- **Driver:** Security
- **Priority:** Must

### Technical Story

**In order to** reduce credential reuse risk in long-running jobs
**The team needs** automatic token rotation for background workers
**So that** worker-driven user stories can execute without violating the platform security policy

### Acceptance Criteria

#### AC-1: Rotation works before token expiry

Given a worker holds a valid service token, when token age reaches the rotation threshold, then:
- the worker refreshes the token before expiry
- in-flight jobs continue without authentication failure

#### AC-2: Security proof exists

Given the rotation mechanism is enabled, when security checks are executed, then:
- expired tokens are rejected
- refreshed tokens are used in subsequent outbound calls
- logs contain non-secret rotation events for audit review
```

## Complete Example Output

```markdown
## TS-PAY-021: Add Idempotency Guard for Payment Callback Processing

### Classification

- **Type:** Architecture
- **Driver:** Reliability
- **Priority:** Must

### References

| Type | Link |
|------|------|
| PRD | Payment callback reliability requirement |
| Architecture | Payments > Webhook Processing |
| SRS | [SRS-PAY-021] |
| Related US | [US-PAY-008] |

### Technical Story

**In order to** prevent duplicate payment state transitions from repeated gateway callbacks
**The team needs** an idempotency guard in the callback processing path
**So that** payment completion stories remain correct and operators do not need manual reconciliation for duplicated webhook deliveries

### Problem Statement

The payment gateway can resend the same callback more than once.
The current processing path does not prove that duplicate deliveries are safely ignored.
This creates risk of double state transition, duplicate ledger writes, or duplicate notification dispatch.

### Scope

- **In scope:** Detect duplicate callback events using a stable callback identity
- **In scope:** Prevent repeated business processing for already-applied callback events
- **In scope:** Record verifiable processing outcome for support and audit review
- **Out of scope:** Full redesign of the payment event model
- **Out of scope:** Gateway contract renegotiation

### Pre-conditions

- Payment callback endpoint already exists
- Payment records have a stable business identifier
- Callback payload contains at least one replay-stable identity field or derivable fingerprint

### Acceptance Criteria

#### AC-1: Duplicate callback does not reapply business state

Given a callback for a payment has already been processed successfully, when the same callback is delivered again, then:
- the system does not create a second successful transition for that payment
- the system does not emit duplicate downstream side effects
- the duplicate delivery is recorded as ignored or already-processed

#### AC-2: First valid callback still completes normally

Given a valid callback for a pending payment is received for the first time, when callback processing runs, then:
- the payment transitions to the expected terminal or next valid state
- the idempotency guard does not block the legitimate first-time callback
- the processing result is traceable in logs or persistence evidence

#### AC-3: Support evidence exists for replay handling

Given duplicate callbacks occur in production or test, when operators inspect the processing trail, then:
- they can distinguish first-time processing from duplicate replay rejection
- the system exposes enough non-secret evidence to explain why the duplicate was not reprocessed

### Evidence

- **Test/Check:** integration test covering first callback + repeated callback replay
- **Metric/Signal:** no increase in duplicate successful state transitions for the same payment identifier
- **Artifact:** callback processing log entry or persistence record showing replay-safe handling

### Risks

- **Risk:** Callback identity may not be truly stable across all gateway retries
- **Mitigation:** Define accepted identity source explicitly and reject weak fallback matching without review

### Follow-up

- [US-PAY-008] remains safe under callback replay conditions
- Optional next story: reconcile late or out-of-order callback delivery handling
```

## Bad Example

```markdown
## TS-AUTH-014: Refactor auth module

Upgrade auth code and clean old logic.
```

Why it fails:
- no bounded outcome
- no business or technical value statement
- no traceability
- no measurable acceptance evidence

## Self-Review Checklist

Trước khi output, verify:

- [ ] Story ID đúng format `TS-XXX-NNN`
- [ ] Story được yêu cầu explicit là `Technical Story` hoặc `Enabler Story`
- [ ] Có đúng 1 technical objective chính
- [ ] Classification dùng đúng loại: Exploration / Architecture / Infrastructure / Compliance
- [ ] Technical value hoặc risk reduction được nói rõ, không vague
- [ ] Có traceability tới ít nhất 1 artifact khác nếu context cho phép
- [ ] Acceptance Criteria mô tả outcome có thể verify, không phải effort
- [ ] Có evidence section hoặc equivalent proof expectation
- [ ] Không biến story thành task list hoặc implementation plan
- [ ] Không có UI copy, visual spec, hoặc code block thừa
- [ ] Nếu context chưa đủ, assumption và open question được tách rõ

**Phát hiện vi phạm -> tự sửa trước khi output.**
