---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer starts or resumes the Pomodoro timer",
      "kind": "actor",
      "entities": [
        {
          "entity": "pomodoro",
          "effect": "reads",
          "facts": [
            "Phase",
            "Remaining time"
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
      "text": "The Product starts the Pomodoro timer countdown",
      "kind": "product",
      "entities": [
        {
          "entity": "pomodoro",
          "effect": "changes",
          "facts": [],
          "from": "Stopped",
          "to": "Running"
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
      "text": "The Product decreases Pomodoro timer Remaining time while running",
      "kind": "product",
      "entities": [
        {
          "entity": "pomodoro",
          "effect": "changes",
          "facts": [
            "Remaining time"
          ]
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
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/context/BoardContext.jsx#BoardProvider"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/server/routes/tasks.js:7-127"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/server/models/Task.js#taskSchema"
    }
  ]
}
---

# Start or resume work countdown

## Trigger

The Developer chooses Focus while the work phase is stopped.

## Outcome

The current work phase advances from its retained remaining time; it does not automatically switch phases on Focus.

## Edge cases

- Starting and resuming use the same Focus control.
- Remaining progress is transient and is not restored after board unmount.
