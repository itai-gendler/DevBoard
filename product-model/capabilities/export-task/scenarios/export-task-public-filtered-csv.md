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
          "place": "devboard-web::public::board"
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
            "Status",
            "Priority",
            "Tags",
            "Created"
          ]
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
      "text": "The Product downloads the requested content",
      "kind": "product",
      "entities": [],
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
      "target": "devboard/client/src/pages/Dashboard.jsx#Dashboard"
    }
  ]
}
---

# Download the filtered collection as CSV

## Trigger

The Developer chooses the corresponding export.

## Outcome

CSV downloads only the currently filtered tasks, with Title, Status, Priority, Tags and Created columns.

## Edge cases

- Exports do not include every task fact or establish an import/restore workflow.
- CSV quotes values, doubles embedded quotes, prefixes spreadsheet-formula-leading characters with an apostrophe, uses the implemented BOM and row separators, and formats valid dates as UTC days.
- Missing or invalid creation dates export as blank; tags join with semicolons.
