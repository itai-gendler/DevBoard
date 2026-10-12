---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer submits the column-name input",
      "kind": "actor",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::public::board"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product appends the trimmed lowercased column name to Board preferences",
      "kind": "product",
      "entities": [
        {
          "entity": "board-preferences",
          "effect": "changes",
          "facts": [
            "Column names"
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

# Add a local column name

## Trigger

The Developer supplies a column name.

## Outcome

The column name is added locally and retained in browser storage; the connected Task status vocabulary is unchanged.

## Edge cases

- Duplicate names are not refused.
- Demo tasks can use custom status values; connected saves to unsupported status values are rejected.
- No column rename/removal lifecycle is inferred.
