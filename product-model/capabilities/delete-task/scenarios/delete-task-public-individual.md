---
{
  "kind": "primary",
  "routes": {
    "web": "Board",
    "editor": "Inline Edit Task"
  },
  "steps": [
    {
      "text": "The Developer confirms removal of one Demo Task from its board card or inline editor while its card tracker is paused",
      "kind": "actor",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "reads",
          "facts": [
            "Title",
            "Status"
          ]
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::public::board"
        },
        "editor": {
          "place": "devboard-web::public::edit-task"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product removes the Demo Task and its contained Code Snippet and histories; their paused mounted Time tracker instances end when the local cards unmount",
      "kind": "product",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "removes"
        },
        {
          "entity": "code-snippet",
          "effect": "removes",
          "with": "demo-task"
        },
        {
          "entity": "recent-activity",
          "effect": "removes",
          "with": "demo-task"
        },
        {
          "entity": "assignee-history",
          "effect": "removes",
          "with": "demo-task"
        },
        {
          "entity": "time-tracker",
          "effect": "removes",
          "as": "demo-task-tracker",
          "from": "Paused",
          "with": "demo-task"
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::public::board"
        },
        "editor": {
          "place": "devboard-web::public::edit-task"
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
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/pages/TaskPage.jsx#TaskPage"
    }
  ]
}
---

# Delete tasks: individual

## Trigger

The Developer confirms removing one Demo Task from its board card or inline editor; its mounted card tracker is paused in this case.

## Outcome

The selected task and its contained code and histories are removed from the current collection. The board card unmounts and its tracker ends; the inline editor closes in the current board.

## Edge cases

- Canceled confirmation removes nothing.
- Deletion also accepts tasks in the other stored states.
- Archive has no recovery or archived lifecycle state.
- Existing local pin records are not automatically cleared.

## Card lifetime

This case removes paused mounted card trackers. A running tracker also ends on card unmount; deletion is not broadcast to other connected clients.

## Linked deletion

A linked task editor has no mounted card tracker to remove. It deletes the task, closes and returns to the board; that hand-off and the newly mounted destination timers are represented in Remove linked task.
