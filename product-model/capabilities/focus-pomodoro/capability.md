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

# Focus Pomodoro

Start or resume the current work/break countdown; phase expiry stops and work expiry can attempt credit to the currently selected task.
