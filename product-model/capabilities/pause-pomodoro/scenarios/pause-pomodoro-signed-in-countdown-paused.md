---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer pauses the Pomodoro timer",
      "kind": "actor",
      "entities": [
        {
          "entity": "pomodoro",
          "effect": "reads",
          "facts": [
            "Remaining time",
            "Phase"
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
      "text": "The Product stops the Pomodoro timer without discarding remaining time",
      "kind": "product",
      "entities": [
        {
          "entity": "pomodoro",
          "effect": "changes",
          "facts": [],
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

# Pause the current countdown

## Trigger

The Developer chooses Pause while the countdown runs.

## Outcome

Countdown advancement stops and the same phase/time can be resumed with Focus.
