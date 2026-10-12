---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "task",
      "facts": [
        "Assignee"
      ],
      "effect": "changes"
    },
    {
      "type": "entity",
      "id": "assignee-history"
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

# Replacing an existing assignee records that previous assignee

When a nonempty replacement differs from an existing Assignee, Assignee history records the prior assignee and replacement time. Initial assignment and clearing do not take this path. The assigning request is outside the mapped web operations; displayed history and this recording constraint reflect the inspected producer.
