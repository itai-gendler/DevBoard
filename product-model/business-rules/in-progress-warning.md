---
{
  "appliesTo": [
    {
      "type": "context",
      "context": {
        "place": "devboard-web::public::board"
      }
    },
    {
      "type": "context",
      "context": {
        "place": "devboard-web::signed-in::board"
      }
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

# More than five visible In Progress tasks produces a warning

More than five visible tasks in the In Progress column produces a WIP warning. It does not prevent creation or movement, and filtering changes the visible count.
