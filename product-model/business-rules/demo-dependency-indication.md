---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "demo-task",
      "facts": [
        "Dependencies",
        "Status"
      ],
      "contexts": [
        {
          "place": "devboard-web::public::board"
        }
      ]
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
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/context/BoardContext.jsx#BoardProvider"
    }
  ]
}
---

# A nonempty demo dependency list contributes blocked indication

Each visible demo task with a nonempty Dependencies list contributes to the column blocked count, regardless of whether referenced tasks are Done. The indication does not prevent any status movement and does not establish cycle prevention or automatic cleanup.
