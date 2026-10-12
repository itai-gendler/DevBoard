---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer confirms removing two Demo Task entries selected in the same column",
      "kind": "actor",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "reads",
          "facts": [
            "Title",
            "Status"
          ],
          "as": "first"
        },
        {
          "entity": "demo-task",
          "effect": "reads",
          "facts": [
            "Title",
            "Status"
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
      "text": "The Product removes both Demo Task entries and their contained Code Snippet, Recent activity and Assignee history data after successful responses; their paused mounted Time tracker instances end when the local cards unmount",
      "kind": "product",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "removes",
          "as": "first"
        },
        {
          "entity": "code-snippet",
          "effect": "removes",
          "with": "first",
          "as": "first-code-snippet"
        },
        {
          "entity": "recent-activity",
          "effect": "removes",
          "with": "first",
          "as": "first-recent-activity"
        },
        {
          "entity": "assignee-history",
          "effect": "removes",
          "with": "first",
          "as": "first-assignee-history"
        },
        {
          "entity": "demo-task",
          "effect": "removes",
          "as": "second"
        },
        {
          "entity": "code-snippet",
          "effect": "removes",
          "with": "second",
          "as": "second-code-snippet"
        },
        {
          "entity": "recent-activity",
          "effect": "removes",
          "with": "second",
          "as": "second-recent-activity"
        },
        {
          "entity": "assignee-history",
          "effect": "removes",
          "with": "second",
          "as": "second-assignee-history"
        },
        {
          "entity": "time-tracker",
          "effect": "removes",
          "as": "first-tracker",
          "from": "Paused",
          "with": "first"
        },
        {
          "entity": "time-tracker",
          "effect": "removes",
          "as": "second-tracker",
          "from": "Paused",
          "with": "second"
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
      "target": "devboard/client/src/components/Task/TaskModal.jsx#TaskModal"
    },
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
      "target": "devboard/client/src/pages/Dashboard.jsx#Dashboard"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/context/BoardContext.jsx#BoardProvider"
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

# Delete tasks: selection

## Trigger

The Developer confirms removing the selected task or group.

## Outcome

The selected task or group is removed from the local collection after successful responses. A linked editor returns to the board.

## Edge cases

- Canceled confirmation removes nothing.
- Deletion also accepts tasks in the other stored states.
- Archive has no recovery or archived lifecycle state.
- Existing local pin records are not automatically cleared.
- Group deletion uses allSettled; failed identifiers remain selected for retry.

## Card lifetime

This case removes paused mounted card trackers. A running tracker also ends on card unmount; deletion is not broadcast to other connected clients.
