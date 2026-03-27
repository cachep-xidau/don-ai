# Function List

Development-ready function documentation with overview table and Main Flow specifications + optional NFR for sprint planning and developer handoff.

## Template

```markdown
# Function List: [Feature Name]

**Feature:** [Feature description]
**Module:** [MODULE-CODE] - [Module Name]
**Total Functions:** [N]

## Function Overview Table

| Function ID | Function Name | Description | Link | Figma |
|-------------|---------------|-------------|------|----------|
| F-XXX-001 | [Name] | [1-sentence description] | [URL or TBD] | [URL or TBD] |

## Detailed Specifications

### F-XXX-001: [Function Name]

**Main Flow:**
1. [High-level step 1]
2. [High-level step 2]
3. [High-level step 3-5]

**NFR:** *(Optional - include only if applicable)*
- **Performance:** Response time, throughput
- **Security:** Authentication, authorization, encryption
- **Reliability:** Uptime, failover, error recovery
- **Scalability:** Concurrent users, data volume
```

**Guidelines:**
- Main Flow: 3-5 high-level steps, avoid excessive UI detail
- NFR: Include only if applicable (Performance, Security, Reliability, Scalability)

## Complete Example

```markdown
# Function List: Widget Customization

## Function Overview Table

| Function ID | Function Name | Description | Link | Figma |
|-------------|---------------|-------------|------|----------|
| F-TOD-010 | Access Widget Customization | Provide easy access to widget settings via Settings icon | TBD | TBD |
| F-TOD-012 | Toggle Widget Visibility | Allow show/hide widgets with minimum 1 visible validation | TBD | TBD |

## Detailed Specifications

### F-TOD-010: Access Widget Customization

**Main Flow:**
1. User taps Settings icon in top-right corner of Today Overview
2. System opens the Customize Dashboard screen
3. System loads current widget preferences
4. System displays the available widget configuration options

**NFR:**
- **Performance:** Dashboard customization screen opens within 200ms
- **Security:** Requires authentication

### F-TOD-012: Toggle Widget Visibility

**Main Flow:**
1. User taps toggle switch for a specific widget
2. System validates whether the change is allowed
3. System updates the widget visibility state
4. System persists the new preference
5. System refreshes the visible widget count

**NFR:**
- **Performance:** Toggle response < 50ms
- **Reliability:** Preference changes are saved without data loss
```

## Writing Guidelines

**Main Flow:**
- 3-5 high-level steps, avoid excessive UI detail
- Focus on user actions and system responses

**Good:** "User taps Settings icon in top-right corner"
**Bad:** "User navigates to settings screen by tapping the gear icon located in the upper right quadrant of the navigation bar"

**NFR (Optional):**
Include only if applicable - Performance, Security, Reliability, Scalability

## What NOT to Include

Function Lists focus on Main Flow + NFR. Exclude:

- **Pre/Post-conditions:** Use User Story sections
- **Alternative/Exception Flows:** Use User Story Exception Handling
- **Business Rules:** Use User Story BR table
- **Detailed Specs:** SQL queries, API calls → SRS document
- **Deploy Time:** Track in Jira/project management
- **Value Statements:** Use Overview Table description column

## Self-Review Checklist

Trước khi output, verify:

- [ ] Main Flow: 3-5 bước, tập trung user action + system response
- [ ] Không quá chi tiết UI (bad: "tap gear icon in upper right quadrant")
- [ ] Không nhét exception branch hoặc implementation internals vào Main Flow
- [ ] NFR: chỉ thêm nếu applicable (Performance/Security/Reliability/Scalability)
- [ ] Không có Business Rules, Exception Flows, Pre/Post-conditions
- [ ] Function ID đúng format `F-XXX-NNN`

**Phát hiện vi phạm → tự sửa trước khi output.**
