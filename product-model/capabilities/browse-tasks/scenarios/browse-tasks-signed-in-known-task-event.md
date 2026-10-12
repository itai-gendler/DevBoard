---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "An update event arrives for a Task already in the current collection",
      "kind": "condition",
      "entities": [
        {
          "entity": "task",
          "effect": "reads",
          "facts": [
            "Title",
            "Description",
            "Notes",
            "Status",
            "Previous status",
            "Priority",
            "Tags",
            "Issue URL",
            "Issue number",
            "Assignee",
            "Due date",
            "Estimate",
            "Order",
            "Pomodoro count",
            "Created",
            "Last changed",
            "Viewers"
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
      "text": "The Product replaces the known cached entry with the incoming Task snapshot",
      "kind": "product",
      "entities": [
        {
          "entity": "task",
          "effect": "reads",
          "facts": [
            "Title",
            "Description",
            "Status",
            "Previous status",
            "Priority",
            "Tags",
            "Issue number",
            "Assignee",
            "Due date",
            "Estimate",
            "Order",
            "Pomodoro count",
            "Created",
            "Last changed",
            "Viewers"
          ]
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
      "target": "devboard/client/src/context/BoardContext.jsx#BoardProvider"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/components/Board/KanbanBoard.jsx#KanbanBoard"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/components/Board/Column.jsx#Column"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/components/Board/TaskCard.jsx#TaskCard"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/pages/TaskPage.jsx#TaskPage"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/hooks/useGithubStars.js#useGithubStars"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/server/index.js:29-100"
    },
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
      "target": "devboard/client/src/components/Heatmap/Heatmap.jsx#countsByDate"
    }
  ]
}
---

# Receive an update for a known task

## Trigger

A task:updated event arrives for an already-known task while the connected board is mounted.

## Outcome

The known cached entry is replaced by the received snapshot. Unknown task events do not insert new cards.

## Edge cases

- The socket handshake has no credential payload and the server broadcasts globally.
- Creation, deletion, import and standalone append/increment routes do not provide corresponding update broadcasts.
