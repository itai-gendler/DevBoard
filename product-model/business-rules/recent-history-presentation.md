---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "recent-activity",
      "facts": [
        "Actions",
        "Times"
      ],
      "effect": "reads",
      "contexts": [
        {
          "place": "devboard-web::public::edit-task"
        },
        {
          "place": "devboard-web::signed-in::edit-task"
        }
      ]
    },
    {
      "type": "entity",
      "id": "assignee-history",
      "facts": [
        "Previous assignees",
        "Replacement times"
      ],
      "effect": "reads",
      "contexts": [
        {
          "place": "devboard-web::public::edit-task"
        },
        {
          "place": "devboard-web::signed-in::edit-task"
        }
      ]
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/components/Task/TaskModal.jsx#TaskModal"
    },
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

# Task details present the latest three entries from each history

Available Recent activity and Assignee history each present their latest three inserted entries in reverse order. Assignee history also reports its total length. Demo history can be inherited from previously loaded snapshots; no demo-generated server recording is promised.
