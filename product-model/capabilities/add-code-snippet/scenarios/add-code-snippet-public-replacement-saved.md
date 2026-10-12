---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer enters nonempty code, explicitly chooses an estimate, leaves Status unchanged and confirms Save",
      "kind": "actor",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "reads",
          "facts": [
            "Title"
          ]
        },
        {
          "entity": "code-snippet",
          "effect": "reads",
          "facts": [
            "Language",
            "Code"
          ],
          "as": "existing-code"
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::public::edit-task"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product saves the current Demo Task form content and replaces the Code Snippet collection with the entered block",
      "kind": "product",
      "entities": [
        {
          "entity": "demo-task",
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
            "Dependencies"
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

# Replace saved code with entered code

## Trigger

The Developer enters nonempty code, chooses an estimate and saves the editor with Status unchanged.

## Outcome

Only the entered snippet remains after normal Save; the current form content (including a chosen estimate) is saved in the same request. In this case the status is unchanged.

## Edge cases

- Normal Save title checks still apply to adding code.
- No entered code leaves the saved snippet list unchanged.
- New-snippet-only input is outside dirty-form detection.
- Other retained code blocks remain when one existing block is removed.
