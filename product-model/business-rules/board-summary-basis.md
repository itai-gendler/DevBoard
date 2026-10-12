---
{
  "appliesTo": [
    {
      "type": "context",
      "context": {
        "place": "devboard-web::public::board"
      }
    },
    {
      "type": "context",
      "context": {
        "place": "devboard-web::signed-in::board"
      }
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/pages/Dashboard.jsx#Dashboard"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/components/Heatmap/Heatmap.jsx#countsByDate"
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
    }
  ]
}
---

# Board summaries derive from the filtered task collection

Board totals and completed counts use the filtered collection. The displayed current-user completion percentage rounds Done divided by tasks matching the optional assignee/current-browser-identity comparison, or zero when there are none; assignment comparison is not ownership. An absent current-account identifier can match an absent assignee identifier, including unassigned demo tasks. Activity Velocity groups currently Done filtered tasks by Created date over the implemented twelve-week window, not by completion time. Column high-priority and snippet totals use the unfiltered tasks in that column; search can therefore make the summary bases differ.
