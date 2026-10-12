---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/server/models/User.js#userSchema"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/server/routes/auth.js:6-57"
    }
  ],
  "relations": [
    {
      "entity": "task",
      "verb": "is assignee of",
      "cardinality": "one-to-many"
    }
  ]
}
---

# Account

A registered identity used to enter connected task work.

## Information kept

- **Name** — The account name.
- **Email** — The account email address.
- **Password** — The secret credential checked at sign-in; it is not disclosed by the board.
