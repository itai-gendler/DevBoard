---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer selects two Demo Task entries for a different order within their column",
      "kind": "actor",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "reads",
          "facts": [
            "Title",
            "Status",
            "Order"
          ],
          "as": "first"
        },
        {
          "entity": "demo-task",
          "effect": "reads",
          "facts": [
            "Title",
            "Status",
            "Order"
          ],
          "as": "second"
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::public::board"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product renumbers both Demo Task entries within the column",
      "kind": "product",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "changes",
          "facts": [
            "Order"
          ],
          "as": "first"
        },
        {
          "entity": "demo-task",
          "effect": "changes",
          "facts": [
            "Order"
          ],
          "as": "second"
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::public::board"
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

# Move task: within column order

## Trigger

The Developer moves work using the board or its status form.

## Outcome

Ordering changes within the column without a new previous-status value or status-change activity.

## Edge cases

- Filtering limits the tasks being renumbered.
- Pinned precedence and priority sorting can alter the apparent order independently.
