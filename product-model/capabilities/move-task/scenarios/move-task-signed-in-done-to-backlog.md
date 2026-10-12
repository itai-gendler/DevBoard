---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer drags the Task between nonempty columns whose visible peer ordering must be renumbered",
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
          "as": "moved"
        },
        {
          "entity": "task",
          "effect": "reads",
          "facts": [
            "Title",
            "Status",
            "Order"
          ],
          "as": "source-peer"
        },
        {
          "entity": "task",
          "effect": "reads",
          "facts": [
            "Title",
            "Status",
            "Order"
          ],
          "as": "destination-peer"
        },
        {
          "entity": "time-tracker",
          "effect": "reads",
          "facts": [
            "Elapsed time"
          ],
          "as": "moved-old-tracker"
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
      "text": "The Task is in Done",
      "kind": "condition",
      "entities": [
        {
          "entity": "task",
          "effect": "reads",
          "facts": [
            "Status"
          ],
          "as": "moved"
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
      "text": "The Product moves the Task into Backlog and independently renumbers the visible source and destination peers without changing their statuses; the moving card Time tracker unmounts and the destination card starts elapsed time at zero",
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
          "from": "Done",
          "to": "Backlog",
          "as": "moved"
        },
        {
          "entity": "task",
          "effect": "changes",
          "facts": [
            "Status",
            "Order",
            "Last changed"
          ],
          "as": "source-peer"
        },
        {
          "entity": "task",
          "effect": "changes",
          "facts": [
            "Status",
            "Order",
            "Last changed"
          ],
          "as": "destination-peer"
        },
        {
          "entity": "time-tracker",
          "effect": "removes",
          "as": "moved-old-tracker",
          "from": "Paused"
        },
        {
          "entity": "time-tracker",
          "effect": "creates",
          "facts": [
            "Elapsed time"
          ],
          "as": "movednew-tracker",
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

# Move task: done to backlog

## Trigger

The Developer moves work using the board or its status form.

## Outcome

The task moves directly from Done to Backlog. Previous status and recent activity reflect the actual change; affected visible ordering is updated through independent requests.

## Edge cases

- The status form offers the same state transition without a mandatory ordering change.
- WIP warnings and dependency selections do not prevent this transition.
- Cross-column requests renumber visible source/destination tasks and can partially complete.
- Mounted card tracking ends when its card unmounts.
- In this case the moving card trackers are paused before the move; running trackers also end on unmount.
