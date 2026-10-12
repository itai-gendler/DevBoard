---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer browses matching task content",
      "kind": "actor",
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
            "Last changed"
          ]
        },
        {
          "entity": "code-snippet",
          "effect": "reads",
          "facts": [
            "Language",
            "Code"
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
      "text": "The Product retains browsing choices and nonempty search history",
      "kind": "product",
      "entities": [
        {
          "entity": "board-preferences",
          "effect": "changes",
          "facts": [
            "Browsing choices",
            "Search history"
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
      "text": "The Product initializes and presents the mounted Pomodoro timer",
      "kind": "product",
      "entities": [
        {
          "entity": "pomodoro",
          "effect": "creates",
          "facts": [
            "Phase",
            "Remaining time",
            "Completed sessions",
            "Remembered sessions",
            "Attached task"
          ],
          "to": "Stopped"
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
      "text": "The Product initializes the mounted card Time tracker",
      "kind": "product",
      "entities": [
        {
          "entity": "time-tracker",
          "effect": "creates",
          "facts": [
            "Elapsed time"
          ],
          "to": "Paused"
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
      "text": "The Product updates board-presence and previous-visit stamps",
      "kind": "product",
      "entities": [
        {
          "entity": "board-preferences",
          "effect": "changes",
          "facts": [
            "Last seen",
            "Previous visit"
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

# Browse and filter the board

## Trigger

The Developer browses the board or resolves the requested task route.

## Outcome

Matching tasks, task metadata, timers, preferences and derived summaries are available. Search, exact tag filtering, priority sorting, pin precedence and focus hiding of Done columns refine browsing.

## Edge cases

- Empty results remain a board outcome.
- Search matches title, description, tags, priority labels and code text case-insensitively; tag filters use exact spelling.
- Nonempty search history is trimmed, case-insensitively deduplicated and limited to five.
- Per-column high-priority/snippet counts use unfiltered tasks while board summaries use filtered tasks.
- Default demo metadata may be absent; seed in_progress can contribute to totals without appearing in a built-in column.
- Task selection changes the timer attachment while the board is mounted.
