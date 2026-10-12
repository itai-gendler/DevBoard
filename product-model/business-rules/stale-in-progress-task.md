---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "task",
      "facts": [
        "Last changed",
        "Status"
      ],
      "contexts": [
        {
          "place": "devboard-web::signed-in::board"
        }
      ]
    },
    {
      "type": "entity",
      "id": "demo-task",
      "facts": [
        "Last changed",
        "Status"
      ],
      "contexts": [
        {
          "place": "devboard-web::public::board"
        }
      ]
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/components/Board/TaskCard.jsx#TaskCard"
    }
  ]
}
---

# In Progress tasks unchanged for seven days are marked stale

An In Progress task is marked stale when the available Last changed time is at least seven days old. Missing change metadata does not synthesize an old time for demo work.
