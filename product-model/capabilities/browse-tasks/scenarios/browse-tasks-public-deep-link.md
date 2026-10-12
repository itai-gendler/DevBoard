---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer opens the ordinary linked route",
      "kind": "actor",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::public::edit-task"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product records the local viewer value when it is not already present",
      "kind": "product",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "changes",
          "facts": [
            "Viewers"
          ]
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::public::edit-task"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product retrieves and presents the known Demo Task content; an existing estimate is not initialized, and a stored timestamp may not populate the date input",
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

# Resolve a linked task and record its viewer

## Trigger

The Developer resolves a cached Demo Task through its ordinary link with a mock viewer value not yet recorded.

## Outcome

A matching cached task becomes available in Edit Task; the detail request records a viewer once when not already present.

## Edge cases

- Local viewer recording changes only the cached Demo Task Viewers; it does not update Last changed or emit a server event.
- The explicit demo profile supplies _id while the local viewer routine reads id, so the recorded value can be invalid.
- Sign-in loses the original task destination and redirects to the board.
- Existing estimate is not initialized into the editor; stored timestamp date input can appear empty.
- Available histories show only their latest three entries.
- QR reveal and dismissal present the ordinary task URL and use the existing route-resolution behavior.

- A mock viewer value already present in the local list is not added again.
