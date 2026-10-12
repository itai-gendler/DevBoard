---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer requests the export",
      "kind": "actor",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "reads",
          "facts": [
            "Title"
          ]
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
      "text": "The Product reads the supported export facts",
      "kind": "product",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "reads",
          "facts": [
            "Title",
            "Description",
            "Status",
            "Priority",
            "Tags",
            "Created"
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
          "place": "devboard-web::public::edit-task"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product requests clipboard writing of the JSON representation",
      "kind": "product",
      "entities": [],
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
      "target": "devboard/client/src/pages/Dashboard.jsx#Dashboard"
    }
  ]
}
---

# Export selected task JSON to the clipboard

## Trigger

The Developer chooses the corresponding export.

## Outcome

JSON contains title, description, status, priority, tags, code blocks and creation time; its success feedback does not await clipboard acceptance.

## Edge cases

- Exports do not include every task fact or establish an import/restore workflow.
