---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer changes the Time tracker running state",
      "kind": "actor",
      "entities": [
        {
          "entity": "time-tracker",
          "effect": "reads",
          "facts": [
            "Elapsed time"
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
      "text": "The Product starts the Time tracker",
      "kind": "product",
      "entities": [
        {
          "entity": "time-tracker",
          "effect": "changes",
          "facts": [],
          "from": "Paused",
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
      "text": "The Product increases Time tracker Elapsed time while the card stays mounted",
      "kind": "product",
      "entities": [
        {
          "entity": "time-tracker",
          "effect": "changes",
          "facts": [
            "Elapsed time"
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
      "target": "devboard/client/src/components/Board/TaskCard.jsx#TaskCard"
    }
  ]
}
---

# Start or resume card elapsed time

## Trigger

The Developer starts/resumes the mounted card tracker.

## Outcome

The mounted card advances retained elapsed seconds.

## Edge cases

- The tracker is independent of Pomodoro task credit.
- Card unmount clears its interval and removes the transient instance; remount starts a new elapsed count.
