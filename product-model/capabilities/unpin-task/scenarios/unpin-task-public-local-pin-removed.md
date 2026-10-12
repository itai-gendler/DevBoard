---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer selects the Demo Task pin operation",
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
      "text": "The Product changes the selected entry in Board preferences",
      "kind": "product",
      "entities": [
        {
          "entity": "board-preferences",
          "effect": "changes",
          "facts": [
            "Pinned tasks"
          ]
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
      "target": "devboard/client/src/components/Board/KanbanBoard.jsx#KanbanBoard"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/components/Board/Column.jsx#Column"
    }
  ]
}
---

# Remove a local task pin

## Trigger

The Developer toggles the selected task pin toward unpinned.

## Outcome

The selected task has its local pin removed.

## Edge cases

- Pin precedence is local, not an account/server setting.
- Moving columns does not guarantee immediate pin reinitialization until a column remount.
- Storage failure does not establish retained persistence.
