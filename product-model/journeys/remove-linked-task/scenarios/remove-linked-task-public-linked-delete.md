---
{
  "kind": "primary",
  "result": "achieved",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer confirms deleting the linked Demo Task",
      "kind": "actor",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "reads",
          "facts": [
            "Title"
          ],
          "as": "removed"
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::public::edit-task"
        }
      },
      "actor": "developer",
      "capability": "delete-task"
    },
    {
      "text": "The Product removes the Demo Task and contained Code Snippet and histories",
      "kind": "product",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "removes",
          "as": "removed"
        },
        {
          "entity": "code-snippet",
          "effect": "removes",
          "with": "removed",
          "as": "removed-code-snippet"
        },
        {
          "entity": "recent-activity",
          "effect": "removes",
          "with": "removed",
          "as": "removed-recent-activity"
        },
        {
          "entity": "assignee-history",
          "effect": "removes",
          "with": "removed",
          "as": "removed-assignee-history"
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::public::edit-task"
        }
      },
      "actor": "developer",
      "capability": "delete-task"
    },
    {
      "text": "The Product closes the linked editor and carries the Developer toward the board",
      "kind": "product",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::public::edit-task"
        }
      },
      "actor": "developer",
      "capability": "delete-task"
    },
    {
      "text": "The Developer browses the remaining collection",
      "kind": "actor",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "reads",
          "facts": [
            "Title",
            "Status"
          ],
          "as": "remaining"
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::public::board"
        }
      },
      "actor": "developer",
      "capability": "browse-tasks"
    },
    {
      "text": "The Product initializes the mounted Pomodoro timer and Time tracker",
      "kind": "product",
      "entities": [
        {
          "entity": "pomodoro",
          "effect": "creates",
          "facts": [
            "Phase",
            "Remaining time",
            "Completed sessions",
            "Remembered sessions",
            "Attached task"
          ],
          "to": "Stopped"
        },
        {
          "entity": "time-tracker",
          "effect": "creates",
          "facts": [
            "Elapsed time"
          ],
          "to": "Paused"
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::public::board"
        }
      },
      "actor": "developer",
      "capability": "browse-tasks"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/pages/TaskPage.jsx#TaskPage"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/components/Task/TaskModal.jsx#TaskModal"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/context/BoardContext.jsx#BoardProvider"
    }
  ]
}
---

# Remove linked task — public linked delete

## Trigger

The Developer reaches an existing task by link and confirms Delete.

## Outcome

The task is removed and the destination board is available. No restoration or archived state is created.
