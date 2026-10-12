---
{
  "kind": "primary",
  "result": "achieved",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer duplicates the linked task using current form content after entering a new code block and choosing an estimate",
      "kind": "actor",
      "entities": [
        {
          "entity": "task",
          "effect": "reads",
          "facts": [
            "Title"
          ],
          "as": "original"
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::edit-task"
        }
      },
      "actor": "developer",
      "capability": "duplicate-task"
    },
    {
      "text": "The Product creates a copied task and its own Code Snippet blocks",
      "kind": "product",
      "entities": [
        {
          "entity": "task",
          "effect": "creates",
          "facts": [
            "Title",
            "Description",
            "Notes",
            "Status",
            "Previous status",
            "Priority",
            "Tags",
            "Issue URL",
            "Due date",
            "Estimate",
            "Order",
            "Pomodoro count",
            "Created",
            "Last changed",
            "Viewers"
          ],
          "as": "copy",
          "to": "Backlog"
        },
        {
          "entity": "code-snippet",
          "effect": "creates",
          "facts": [
            "Language",
            "Code"
          ],
          "as": "copied-code",
          "with": "copy"
        },
        {
          "entity": "code-snippet",
          "effect": "creates",
          "facts": [
            "Language",
            "Code"
          ],
          "as": "copied-entered-code",
          "with": "copy"
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::edit-task"
        }
      },
      "actor": "developer",
      "capability": "duplicate-task"
    },
    {
      "text": "The Product closes the linked editor and carries the Developer toward the board",
      "kind": "product",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::edit-task"
        }
      },
      "actor": "developer",
      "capability": "duplicate-task"
    },
    {
      "text": "The Developer browses the copy on the destination board",
      "kind": "actor",
      "entities": [
        {
          "entity": "task",
          "effect": "reads",
          "facts": [
            "Title",
            "Status"
          ],
          "as": "copy"
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::board"
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
          "place": "devboard-web::signed-in::board"
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

# Copy linked task — signed in linked copy

## Trigger

The Developer reaches an existing task by link and chooses Duplicate.

## Outcome

The independent copy appears on the board after the linked editor closes. Issue linkage is excluded, dependencies are cleared, and existing/new code is combined.
