---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The running Pomodoro timer reaches phase expiry",
      "kind": "condition",
      "entities": [
        {
          "entity": "pomodoro",
          "effect": "reads",
          "facts": [
            "Phase",
            "Remaining time",
            "Completed sessions",
            "Attached task"
          ]
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::board"
        }
      },
      "unattended": true
    },
    {
      "text": "The Product stops the Pomodoro timer and initializes the next phase",
      "kind": "product",
      "entities": [
        {
          "entity": "pomodoro",
          "effect": "changes",
          "facts": [
            "Phase",
            "Remaining time",
            "Completed sessions",
            "Remembered sessions"
          ],
          "from": "Running",
          "to": "Stopped"
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::board"
        }
      }
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

# Finish work without an attached task

## Trigger

The running work countdown reaches expiry.

## Outcome

Completed and remembered work counts increase; the next break is initialized stopped and no task write is attempted.

## Edge cases

- Work phases last 25 minutes; breaks are five minutes except the 15-minute break after every fourth completed work session.
- Attachment uses current selection at expiry, not a durable task assignment or guaranteed original focus target.
- Task credit is not atomic, exactly once or protected against concurrent overwrites.
