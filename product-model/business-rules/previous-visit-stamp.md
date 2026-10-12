---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "board-preferences",
      "facts": [
        "Last seen",
        "Previous visit"
      ],
      "contexts": [
        {
          "place": "devboard-web::public::board"
        },
        {
          "place": "devboard-web::signed-in::board"
        }
      ]
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/utils/lastVisit.js#openVisit"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/utils/lastVisit.js#touchVisit"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/pages/Dashboard.jsx#Dashboard"
    }
  ]
}
---

# A separated visit retains the previous last-seen stamp

On opening after a gap greater than thirty minutes, a valid preceding Last seen stamp becomes Previous visit; this is the last observed presence, not the preceding session start. Last seen advances at opening and every minute while the board is mounted. Missing/invalid prior data does not create a prior-visit time; guarded storage failure can omit retention.
