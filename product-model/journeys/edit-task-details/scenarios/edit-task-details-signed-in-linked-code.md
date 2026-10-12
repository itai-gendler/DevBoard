---
{
  "kind": "primary",
  "result": "achieved",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer enters nonempty code, explicitly chooses an estimate, leaves Status unchanged and confirms Save",
      "kind": "actor",
      "entities": [
        {
          "entity": "task",
          "effect": "reads",
          "facts": [
            "Title"
          ]
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::edit-task"
        }
      },
      "actor": "developer",
      "capability": "add-code-snippet"
    },
    {
      "text": "The Product saves the current task form content and replaces the Code Snippet collection with the entered block",
      "kind": "product",
      "entities": [
        {
          "entity": "task",
          "effect": "changes",
          "facts": [
            "Title",
            "Description",
            "Notes",
            "Status",
            "Priority",
            "Tags",
            "Issue URL",
            "Issue number",
            "Due date",
            "Estimate",
            "Last changed"
          ]
        },
        {
          "entity": "code-snippet",
          "effect": "removes",
          "as": "existing-code"
        },
        {
          "entity": "code-snippet",
          "effect": "creates",
          "facts": [
            "Language",
            "Code"
          ],
          "as": "entered"
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::edit-task"
        }
      },
      "actor": "developer",
      "capability": "add-code-snippet"
    },
    {
      "text": "The Product completes the editor and carries the Developer back toward the board",
      "kind": "product",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::edit-task"
        }
      },
      "actor": "developer",
      "capability": "add-code-snippet"
    },
    {
      "text": "The Developer browses the resulting board",
      "kind": "actor",
      "entities": [
        {
          "entity": "task",
          "effect": "reads",
          "facts": [
            "Title",
            "Status"
          ]
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
      "text": "The Product initializes the board Pomodoro timer and Time tracker",
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

# Edit task details — signed in linked code

## Trigger

The Developer enters code and chooses an estimate in a linked task editor, retaining its current Status.

## Outcome

The current form content and replacement code are saved together, and the Developer finishes at the board. The linked-editor Save callback performs the return hand-off.
