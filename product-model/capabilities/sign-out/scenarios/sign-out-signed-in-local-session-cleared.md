---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer confirms local sign-out",
      "kind": "actor",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::board"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product clears browser identity, cached collection and search query",
      "kind": "product",
      "entities": [
        {
          "entity": "board-preferences",
          "effect": "changes",
          "facts": [
            "Browsing choices"
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
      "text": "The Product removes the mounted Pomodoro timer and Time tracker instances",
      "kind": "product",
      "entities": [
        {
          "entity": "pomodoro",
          "effect": "removes",
          "from": "Stopped"
        },
        {
          "entity": "time-tracker",
          "effect": "removes",
          "from": "Paused"
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
      "target": "devboard/client/src/context/BoardContext.jsx#BoardProvider"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/pages/Dashboard.jsx#Dashboard"
    }
  ]
}
---

# Clear the current browser session after confirmation

## Trigger

The Developer confirms Sign out on the board while the Pomodoro timer is stopped and the card trackers are paused in this case.

## Outcome

Local access ends and the route guard carries the browser to account access. Issued server credentials are not revoked.

## Edge cases

- Canceling confirmation keeps the browser session.
- Running timers and trackers also end on unmount; pins, columns, search history and visit stamps are not cleared.
- A later fresh initialization can enter default Demo Mode again.
