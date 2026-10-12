---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "pomodoro",
      "facts": [
        "Phase",
        "Remaining time",
        "Completed sessions"
      ]
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

# Pomodoro uses its work and break cycle and stops at phase boundaries

Work lasts 25 minutes. Breaks last five minutes, except a 15-minute break after every fourth completed work session. Expiry stops the timer at the next phase; another Focus act starts it. Work expiry increments the current and remembered counts; break expiry does not. Reset clears current count without immediately overwriting Remembered sessions.
