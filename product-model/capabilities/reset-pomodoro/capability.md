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

# Reset Pomodoro

Reset the current countdown and completed-session count without immediately clearing remembered browser sessions.
