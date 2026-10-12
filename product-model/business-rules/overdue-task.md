---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "task",
      "facts": [
        "Due date",
        "Status"
      ],
      "contexts": [
        {
          "place": "devboard-web::signed-in::board"
        }
      ]
    },
    {
      "type": "entity",
      "id": "demo-task",
      "facts": [
        "Due date",
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
      "target": "devboard/client/src/components/Board/TaskCard.jsx#TaskCard"
    }
  ]
}
---

# A dated task before local today is overdue unless Done

When Due date is present and earlier than local midnight for today, the card is indicated overdue unless Status is Done. Absent dates produce no overdue indication.
