---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer resets the Pomodoro timer",
      "kind": "actor",
      "entities": [
        {
          "entity": "pomodoro",
          "effect": "reads",
          "facts": [
            "Phase",
            "Remaining time",
            "Completed sessions"
          ]
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::board"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product resets the Pomodoro timer current phase and count",
      "kind": "product",
      "entities": [
        {
          "entity": "pomodoro",
          "effect": "changes",
          "facts": [
            "Phase",
            "Remaining time",
            "Completed sessions"
          ],
          "from": "Running",
          "to": "Stopped"
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::board"
        }
      },
      "actor": "developer"
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

# Reset the current cycle without clearing remembered sessions

## Trigger

The Developer resets the running timer.

## Outcome

The timer is stopped at 25-minute Work with current completed sessions zero. Remembered sessions are not immediately rewritten.

## Edge cases

- Reset also applies when the timer is already stopped.
- Remount can restore the remembered count while remaining progress starts again.
