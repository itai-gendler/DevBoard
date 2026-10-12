---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer selects two Task entries for a different order within their column",
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
          "as": "first"
        },
        {
          "entity": "task",
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
          "place": "devboard-web::signed-in::board"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product renumbers both Task entries within the column",
      "kind": "product",
      "entities": [
        {
          "entity": "task",
          "effect": "changes",
          "facts": [
            "Order",
            "Last changed"
          ],
          "as": "first"
        },
        {
          "entity": "task",
          "effect": "changes",
          "facts": [
            "Order",
            "Last changed"
          ],
          "as": "second"
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

# Move task: within column order

## Trigger

The Developer moves work using the board or its status form.

## Outcome

Ordering changes within the column without a new previous-status value or status-change activity.

## Edge cases

- Filtering limits the tasks being renumbered.
- Pinned precedence and priority sorting can alter the apparent order independently.
