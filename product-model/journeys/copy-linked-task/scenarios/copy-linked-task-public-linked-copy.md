---
{
  "kind": "primary",
  "result": "achieved",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer duplicates the linked Demo Task using current form content after entering a new code block and choosing an estimate",
      "kind": "actor",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "reads",
          "facts": [
            "Title"
          ],
          "as": "original"
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::public::edit-task"
        }
      },
      "actor": "developer",
      "capability": "duplicate-task"
    },
    {
      "text": "The Product creates a copied Demo Task and its own Code Snippet blocks",
      "kind": "product",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "creates",
          "facts": [
            "Title",
            "Description",
            "Notes",
            "Status",
            "Priority",
            "Tags",
            "Due date",
            "Estimate",
            "Dependencies",
            "Pomodoro count"
          ],
          "as": "copy"
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
          "place": "devboard-web::public::edit-task"
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
          "place": "devboard-web::public::edit-task"
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
          "entity": "demo-task",
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

# Copy linked task — public linked copy

## Trigger

The Developer reaches an existing task by link and chooses Duplicate.

## Outcome

The independent copy appears on the board after the linked editor closes. Issue linkage is excluded, dependencies are cleared, and existing/new code is combined.
