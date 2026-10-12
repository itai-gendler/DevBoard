---
{
  "availability": [
    {
      "place": "devboard-web::public"
    },
    {
      "place": "devboard-web::signed-in"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/hooks/usePomodoro.js#usePomodoro"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/pages/Dashboard.jsx#handleSessionComplete"
    }
  ]
}
---

# Pause Pomodoro

Stop countdown advancement while retaining current remaining time.
