---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer requests the code change",
      "kind": "actor",
      "entities": [
        {
          "entity": "task",
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
          ]
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::edit-task"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product removes the selected Code Snippet immediately",
      "kind": "product",
      "entities": [
        {
          "entity": "task",
          "effect": "changes",
          "facts": [
            "Last changed"
          ]
        },
        {
          "entity": "code-snippet",
          "effect": "removes"
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::edit-task"
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

# Remove a selected saved code block

## Trigger

The Developer selects an existing code block for removal.

## Outcome

The selected block is removed immediately and remains removed even if later unsaved form changes are discarded.

## Edge cases

- A failed update does not complete local removal.
- Removal does not wait for a later normal Save.
