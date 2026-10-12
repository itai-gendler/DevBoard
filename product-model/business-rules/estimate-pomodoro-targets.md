---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "task",
      "facts": [
        "Estimate",
        "Pomodoro count"
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
        "Estimate",
        "Pomodoro count"
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

# Shipped estimates determine the displayed session target

Estimate values 30m, 1h, 2h, 4h and 1d map respectively to 1, 2, 4, 8 and 16 Pomodoro sessions. Other estimate text has no mapped session target. Actual count remains separately displayed and is not a guaranteed measure of tracked elapsed time.
