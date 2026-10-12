---
{
  "kind": "edge",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer opens the board",
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
      "text": "The outbound GitHub project-star request fails",
      "kind": "condition",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::board"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product continues task browsing with its safe star fallback",
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

# Keep browsing when project stars fail

## Trigger

The Developer browses the board or resolves the requested task route.

## Outcome

Task work remains available and no project-star count is promised.
