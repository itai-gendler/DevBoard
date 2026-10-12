---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "task",
      "facts": [
        "Tags"
      ],
      "effect": "creates"
    },
    {
      "type": "entity",
      "id": "task",
      "facts": [
        "Tags"
      ],
      "effect": "changes"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/server/routes/tasks.js:7-127"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/server/models/Task.js#taskSchema"
    }
  ]
}
---

# Stored tags contain trimmed nonempty exactly deduplicated strings

Stored Tags accept string entries, trim whitespace, remove empty entries and deduplicate exact spellings. Case is preserved; differently cased strings are not universally merged. Demo saves do not promise the same server normalization.
