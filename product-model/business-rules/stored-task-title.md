---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "task",
      "facts": [
        "Title"
      ],
      "effect": "creates"
    },
    {
      "type": "entity",
      "id": "task",
      "facts": [
        "Title"
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

# Stored tasks require a nonempty trimmed title

Stored Title is required and trimmed. The server does not impose the normal form duplicate-title check on all writes.
