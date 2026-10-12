---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "task",
      "facts": [
        "Status"
      ],
      "effect": "changes",
      "contexts": [
        {
          "place": "devboard-web::signed-in"
        }
      ]
    },
    {
      "type": "entity",
      "id": "recent-activity"
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

# Stored status changes retain previous status and record activity

An actual status change through the mapped UI remembers the previous value and records a status-change action/time in Recent activity. An unchanged status records no new status-change entry. Incoming previousStatus and seenBy updates are stripped. Raw history replacement remains possible in the general update payload, so this is not an immutable audit guarantee.
