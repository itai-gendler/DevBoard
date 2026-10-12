---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer selects two Task entries and their destination column",
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
        },
        {
          "entity": "time-tracker",
          "effect": "reads",
          "facts": [
            "Elapsed time"
          ],
          "as": "first-old-tracker"
        },
        {
          "entity": "time-tracker",
          "effect": "reads",
          "facts": [
            "Elapsed time"
          ],
          "as": "second-old-tracker"
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
      "text": "The Product moves both Task entries to the destination with consecutive appended ordering values; the moving card Time tracker unmounts and the destination card starts elapsed time at zero",
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
          "as": "first"
        },
        {
          "entity": "task",
          "effect": "changes",
          "facts": [
            "Status",
            "Previous status",
            "Order",
            "Last changed"
          ],
          "as": "second"
        },
        {
          "entity": "time-tracker",
          "effect": "removes",
          "as": "first-old-tracker",
          "from": "Paused"
        },
        {
          "entity": "time-tracker",
          "effect": "creates",
          "facts": [
            "Elapsed time"
          ],
          "as": "firstnew-tracker",
          "to": "Paused"
        },
        {
          "entity": "time-tracker",
          "effect": "removes",
          "as": "second-old-tracker",
          "from": "Paused"
        },
        {
          "entity": "time-tracker",
          "effect": "creates",
          "facts": [
            "Elapsed time"
          ],
          "as": "secondnew-tracker",
          "to": "Paused"
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

# Move task: selection moved

## Trigger

The Developer moves work using the board or its status form.

## Outcome

Selected entries move to the destination using separately issued updates; no atomic batch guarantee.

## Edge cases

- The destination order starts after the maximum currently filtered destination order.
- No selection or a destination equal to the source initiates no move.
- In this case the moving card trackers are paused before the move; running trackers also end on unmount.
