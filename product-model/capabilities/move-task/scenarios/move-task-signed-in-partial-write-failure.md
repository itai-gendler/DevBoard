---
{
  "kind": "edge",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer selects two Backlog Task entries to move to In Progress",
      "kind": "actor",
      "entities": [
        {
          "entity": "task",
          "effect": "reads",
          "facts": [
            "Title",
            "Status",
            "Order"
          ],
          "as": "saved"
        },
        {
          "entity": "task",
          "effect": "reads",
          "facts": [
            "Title",
            "Status",
            "Order"
          ],
          "as": "failed"
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::board"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product saves a Task update from the group",
      "kind": "product",
      "entities": [
        {
          "entity": "task",
          "effect": "changes",
          "facts": [
            "Status",
            "Previous status",
            "Order",
            "Last changed"
          ],
          "as": "saved",
          "from": "Backlog",
          "to": "In Progress"
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::board"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The other request fails and its Task retains its former status and ordering",
      "kind": "condition",
      "entities": [
        {
          "entity": "task",
          "effect": "reads",
          "facts": [
            "Status",
            "Order"
          ],
          "as": "failed"
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::board"
        }
      },
      "actor": "developer"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/components/Board/KanbanBoard.jsx#KanbanBoard"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/components/Board/Column.jsx#Column"
    },
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
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/context/BoardContext.jsx#BoardProvider"
    }
  ]
}
---

# Move task: partial write failure

## Trigger

The Developer moves work using the board or its status form.

## Outcome

Some persisted moves or order values can remain saved while another request fails; there is no rollback.
