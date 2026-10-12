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
          "place": "devboard-web::public::board"
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
          "place": "devboard-web::public::board"
        }
      }
    },
    {
      "text": "The selected Demo Task supplies the previous Pomodoro count",
      "kind": "condition",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "reads",
          "facts": [
            "Pomodoro count"
          ]
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::public::board"
        }
      }
    },
    {
      "text": "The Product saves the selected Demo Task count plus one",
      "kind": "product",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "changes",
          "facts": [
            "Pomodoro count"
          ]
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::public::board"
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

# Credit the task selected at work expiry

## Trigger

The running work countdown reaches expiry.

## Outcome

The completed work count and remembered count advance, the break is stopped, and a successful update credits the task selected at expiry using an absolute previous-count-plus-one value.

## Edge cases

- Work phases last 25 minutes; breaks are five minutes except the 15-minute break after every fourth completed work session.
- Attachment uses current selection at expiry, not a durable task assignment or guaranteed original focus target.
- Task credit is not atomic, exactly once or protected against concurrent overwrites.
