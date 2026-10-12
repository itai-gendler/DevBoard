---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer opens the selected card",
      "kind": "actor",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "reads",
          "facts": [
            "Title"
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
      "text": "The Product attaches the mounted Pomodoro timer to the current board selection",
      "kind": "product",
      "entities": [
        {
          "entity": "pomodoro",
          "effect": "changes",
          "facts": [
            "Attached task"
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
      "text": "The Product presents the selected Demo Task content; an existing estimate is not initialized, and a stored timestamp may not populate the date input",
      "kind": "product",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "reads",
          "facts": [
            "Title",
            "Description",
            "Notes",
            "Status",
            "Priority",
            "Tags",
            "Issue URL",
            "Issue number",
            "Due date"
          ]
        },
        {
          "entity": "code-snippet",
          "effect": "reads",
          "facts": [
            "Language",
            "Code"
          ]
        },
        {
          "entity": "recent-activity",
          "effect": "reads",
          "facts": [
            "Actions",
            "Times"
          ]
        },
        {
          "entity": "assignee-history",
          "effect": "reads",
          "facts": [
            "Previous assignees",
            "Replacement times"
          ]
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::public::edit-task"
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

# Open details from an existing card

## Trigger

The Developer browses the board or resolves the requested task route.

## Outcome

The selected task is available in Edit Task. Opening the board card does not call the defined viewer-recording handler.

## Edge cases

- Existing estimate is not initialized into the editor; stored timestamp date input can appear empty.
- Available histories show only their latest three entries.
- QR reveal and dismissal present the ordinary task URL and use the existing route-resolution behavior.
