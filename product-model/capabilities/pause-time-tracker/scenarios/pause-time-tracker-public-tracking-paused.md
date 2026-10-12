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
          "place": "devboard-web::public::board"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product pauses the Time tracker",
      "kind": "product",
      "entities": [
        {
          "entity": "time-tracker",
          "effect": "changes",
          "facts": [],
          "from": "Running",
          "to": "Paused"
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::public::board"
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

# Pause card elapsed time

## Trigger

The Developer pauses the mounted card tracker.

## Outcome

The mounted card retains its elapsed seconds without further increments.

## Edge cases

- The tracker is independent of Pomodoro task credit.
- Card unmount clears its interval and removes the transient instance; remount starts a new elapsed count.
