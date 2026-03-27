# ERD with dbdiagram.io (DBML)

Design Entity Relationship Diagrams using DBML syntax for dbdiagram.io.

## Quick Reference

| Element | Syntax | Example |
|---------|--------|---------|
| Table | `Table name {}` | `Table users {}` |
| Column | `name type [settings]` | `id int [pk, increment]` |
| Many-to-One | `>` | `posts.user_id > users.id` |
| One-to-Many | `<` | `users.id < posts.user_id` |
| One-to-One | `-` | `users.id - profiles.user_id` |
| Many-to-Many | Junction table | See Relationships section |
| Index | `indexes { col }` | `indexes { email [unique] }` |
| Enum | `enum name {}` | `enum status { active, inactive }` |
| Note | `[note: 'text']` | `id int [note: 'Primary key']` |

## Column Settings

| Setting | Description |
|---------|-------------|
| `pk` | Primary key |
| `increment` | Auto-increment |
| `not null` | Required field |
| `null` | Nullable field |
| `unique` | Unique constraint |
| `default: value` | Default value |
| `note: 'text'` | Documentation |
| `ref: > table.col` | Inline relationship |

## Table Syntax

```dbml
Table users {
    id int [pk, increment]
    email varchar [unique, not null]
    name varchar [not null]
    role user_role [default: 'user']
    created_at timestamp [default: `now()`]
    updated_at timestamp
}
```

**With Schema:**
```dbml
Table core.users {
    id int [pk, increment]
}
```

## Relationships

### Many-to-One (Most Common)
```dbml
// Many posts belong to one user
Table posts {
    id int [pk]
    user_id int [ref: > users.id, not null]
}

// Or separate definition
Ref: posts.user_id > users.id
```

### One-to-One
```dbml
// One user has one profile
Table profiles {
    id int [pk]
    user_id int [ref: - users.id, unique]
}
```

### Many-to-Many (Junction Table)
```dbml
Table posts {
    id int [pk]
}

Table tags {
    id int [pk]
}

Table post_tags {
    post_id int [ref: > posts.id]
    tag_id int [ref: > tags.id]

    indexes {
        (post_id, tag_id) [pk]
    }
}
```

## Indexes

```dbml
Table orders {
    id int [pk]
    user_id int
    status varchar
    created_at timestamp

    indexes {
        user_id                          // Simple index
        created_at [name: 'idx_created'] // Named index
        (user_id, status)                // Composite index
        (user_id, created_at) [unique]   // Unique composite
        status [type: hash]              // Hash index
    }
}
```

## Enums

```dbml
enum user_role {
    admin
    user
    guest
}

enum order_status {
    pending [note: 'Awaiting payment']
    paid
    shipped
    delivered
    cancelled
}

Table users {
    id int [pk]
    role user_role [default: 'user']
}
```

## Data Types

| Type | Use Case |
|------|----------|
| `int`, `bigint` | Integers, IDs |
| `varchar`, `varchar(255)` | Short strings |
| `text` | Long text content |
| `boolean` | True/false flags |
| `decimal(10,2)` | Money, precise decimals |
| `date` | Calendar dates |
| `timestamp`, `datetime` | Date and time |
| `json`, `jsonb` | JSON data |
| `uuid` | Unique identifiers |

## Best Practices

**Naming:**
- Follow the project's existing naming convention first
- If no convention exists, prefer lowercase with underscores: `user_id`, `created_at`
- Descriptive FK names: `author_id` not `aid`

**Structure:**
- Use the primary key strategy that matches source truth
- `id int [pk, increment]` is common, not mandatory
- Add `created_at`, `updated_at`, or `deleted_at` only when the source context or project convention supports them

**Relationships:**
- Always define FK constraints
- Index all foreign keys
- Use `not null` for required relationships

**Modeling discipline:**
- Do not redesign an inherited schema just to match a style preference
- Composite keys and natural keys are valid if the source context requires them
- If schema details are missing, mark them as assumptions instead of inventing fields

## Self-Review Checklist

Trước khi output, verify:

- [ ] Table names và column names follow source truth or explicit project convention
- [ ] Primary key strategy matches context instead of defaulting blindly to `id`
- [ ] Foreign keys are explicit and relationship direction is correct
- [ ] Junction tables are used for many-to-many where appropriate
- [ ] Invented fields are not introduced without being marked as assumptions
- [ ] Diagram reflects the requested scope, not a speculative full-system redesign

**Phát hiện vi phạm → tự sửa trước khi output.**

## Resources

- [DBML Docs](https://dbml.dbdiagram.io/docs/)
- [dbdiagram.io](https://dbdiagram.io/)
