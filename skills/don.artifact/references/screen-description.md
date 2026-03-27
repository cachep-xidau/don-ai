# Screen Description

Write screen specifications with 3-section structure: Overview, Fields, Action Buttons.

---

## CRITICAL: Exact Text Capture

**ALWAYS capture UI text EXACTLY as shown in Figma.** Never paraphrase, translate, or modify.

| Element | Capture Exactly |
|---------|-----------------|
| Button labels | `"Log In"`, `"Sign Up"`, `"Submit Order"` |
| Field labels | `"Email Address"`, `"Password"` |
| Placeholder text | `"Enter your email"`, `"Select an option"` |
| Helper text | `"We'll never share your email"` |
| Error messages | `"Invalid email format"` |
| Tooltip text | `"Collect duplicate pieces to exchange"` |
| Tab names | `"Gacha"`, `"History"`, `"Settings"` |
| Badge labels | `"New"`, `"Success"`, `"Pending"` |

**Format:** Use `"..."` quotes for exact Figma text in Label column.

---

## Quick Start

```markdown
# Login Screen

**Figma:** [link]

## Overview
User authentication entry point.

## Fields

| Field Name | Label | Data Type | DB Map | Description & Rules |
|------------|-------|-----------|--------|---------------------|
| email-input | `"メールアドレス"` | Text | `users.email` | Required. Valid email format. Max 64 chars |
| password-input | `"パスワード"` | Password | `users.password_hash` | Required. Min 8 chars |

## Action Buttons

| Button Name | Label | Type | Description & Rules |
|-------------|-------|------|---------------------|
| login-btn | `"ログイン"` | Primary | Submit credentials. Disabled if validation fails |
| forgot-password-link | `"パスワードを忘れた場合"` | Link | Navigate to password reset screen |
```

---

## Template

### Single Screen

```markdown
# [Screen Name]

**Figma:** [Design link]

## Overview
[1-2 sentence description of screen purpose]

## Fields

| Field Name | Label | Data Type | DB Map | Description & Rules |
|------------|-------|-----------|--------|---------------------|
| [name] | `"Figma text"` | [type] | [Table.field] | [validation, behavior] |

## Action Buttons

| Button Name | Label | Type | Description & Rules |
|-------------|-------|------|---------------------|
| [name] | `"Figma text"` | [type] | [action/navigation] |
```

---

## Column Definitions

### Fields Table

| Column | Description | Format |
|--------|-------------|--------|
| **Field Name** | Internal identifier | kebab-case (e.g., `email-input`) |
| **Label** | Exact Figma text | `"メールアドレス"`, `-` if none |
| **Data Type** | Input type | Text, Number, Select, Date, Boolean, Password, Display |
| **DB Map** | Database field | `users.email`, `N/A` if calculated |
| **Description & Rules** | Validation, behavior | Required, max length, format, conditional logic |

### Action Buttons Table

| Column | Description | Format |
|--------|-------------|--------|
| **Button Name** | Internal identifier | kebab-case (e.g., `submit-btn`) |
| **Label** | Exact Figma text | `"送信"`, `"キャンセル"` |
| **Type** | Button variant | Primary, Secondary, Link, Icon, Tab |
| **Description & Rules** | Action, conditions | Navigate to X, Disabled if Y, Triggers Z |

---

## Complete Example

```markdown
# Gacha Main Screen

**Figma:** [Link](https://www.figma.com/design/xxx?node-id=945-16786)

## Overview
Main entry point for Gacha system. Select Premium/Regular machines, view tickets.

## Fields

| Field Name | Label | Data Type | DB Map | Description & Rules |
|------------|-------|-----------|--------|---------------------|
| gacha-type-tabs | `"Gacha"`, `"Subscription"` | Select | N/A | Tab selection. Default: Gacha |
| premium-ticket-count | `"x15"` | Display | `user_gacha_tickets.premium_count` | Available Premium tickets |
| regular-ticket-count | `"x3"` | Display | `user_gacha_tickets.regular_count` | Available Regular tickets |
| machine-status | `"Premium"`, `"Regular"` | Display | `gacha_machines.type` | Active machine indicator |
| history-preview | `-` | List | `gacha_history (JOIN items)` | Last 3 opened cards. Relative time format such as `"5m ago"` |

## Action Buttons

| Button Name | Label | Type | Description & Rules |
|-------------|-------|------|---------------------|
| select-premium-btn | `"Premium"` | Primary | Activate Premium machine. Disabled if tickets = 0 |
| select-regular-btn | `"Regular"` | Secondary | Activate Regular machine. Disabled if tickets = 0 |
| view-all-history-link | `"View All"` | Link | Navigate to Gacha History screen |
| gacha-tab | `"Gacha"` | Tab | Current screen (active state) |
| subscription-tab | `"Subscription"` | Tab | Navigate to Subscription screen |
```

---

## What NOT to Include

Screen descriptions focus on **data and behavior**, not visual implementation.

| Exclude | Reason | Where Instead |
|---------|--------|---------------|
| Colors, hex codes | Design system tokens | Figma |
| Font sizes, weights | Typography tokens | Figma |
| Padding, margin, gap | Spacing tokens | Figma |
| Border radius, shadows | Visual effects | Figma |
| Component names | Implementation detail | Dev specs |

> **Rule:** If it changes when design system updates, it doesn't belong here.

---

## DB Map Notation

| Scenario | Format | Example |
|----------|--------|---------|
| Direct field | `Table.column` | `users.email` |
| Calculated | `N/A` | Age from birthdate |
| Composite | `Table.field1 + field2` | `orders.id + items.name` |
| External API | `API: service.field` | `API: stripe.customer_id` |
| Display only | `N/A` | Decorative text |

## Self-Review Checklist

Trước khi output, verify:

- [ ] UI text capture **exact** từ Figma (dùng `"..."`)
- [ ] Field Name và Button Name dùng internal identifier dạng `kebab-case`
- [ ] Fields table: 5 cột đầy đủ (Field Name, Label, Data Type, DB Map, Rules)
- [ ] Action Buttons table: 4 cột đầy đủ (Button Name, Label, Type, Rules)
- [ ] DB Map điền đúng notation (`Table.column`, `N/A`, `API: service.field`)
- [ ] Không có visual properties (color, radius, shadow, spacing)

**Phát hiện vi phạm → tự sửa trước khi output.**
