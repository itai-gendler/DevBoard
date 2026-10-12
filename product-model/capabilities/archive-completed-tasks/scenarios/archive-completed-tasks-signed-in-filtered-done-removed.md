---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer confirms removing two Done Task entries matching the current search and tag filter",
      "kind": "actor",
      "entities": [
        {
          "entity": "task",
          "effect": "reads",
          "facts": [
            "Title",
            "Status"
          ],
          "as": "first"
        },
        {
          "entity": "task",
          "effect": "reads",
          "facts": [
            "Title",
            "Status"
          ],
          "as": "second"
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
      "text": "Both Task entries are Done and in the filtered collection",
      "kind": "condition",
      "entities": [
        {
          "entity": "task",
          "effect": "reads",
          "facts": [
            "Title",
            "Status"
          ],
          "as": "first"
        },
        {
          "entity": "task",
          "effect": "reads",
          "facts": [
            "Title",
            "Status"
          ],
          "as": "second"
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
      "text": "The Product removes both Task entries and their contained Code Snippet, Recent activity and Assignee history data after successful responses; their paused mounted Time tracker instances end when the local cards unmount",
      "kind": "product",
      "entities": [
        {
          "entity": "task",
          "effect": "removes",
          "from": "Done",
          "as": "first"
        },
        {
          "entity": "code-snippet",
          "effect": "removes",
          "with": "first",
          "as": "first-code-snippet"
        },
        {
          "entity": "recent-activity",
          "effect": "removes",
          "with": "first",
          "as": "first-recent-activity"
        },
        {
          "entity": "assignee-history",
          "effect": "removes",
          "with": "first",
          "as": "first-assignee-history"
        },
        {
          "entity": "task",
          "effect": "removes",
          "from": "Done",
          "as": "second"
        },
        {
          "entity": "code-snippet",
          "effect": "removes",
          "with": "second",
          "as": "second-code-snippet"
        },
        {
          "entity": "recent-activity",
          "effect": "removes",
          "with": "second",
          "as": "second-recent-activity"
        },
        {
          "entity": "assignee-history",
          "effect": "removes",
          "with": "second",
          "as": "second-assignee-history"
        },
        {
          "entity": "time-tracker",
          "effect": "removes",
          "as": "first-tracker",
          "from": "Paused",
          "with": "first"
        },
        {
          "entity": "time-tracker",
          "effect": "removes",
          "as": "second-tracker",
          "from": "Paused",
          "with": "second"
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
      "target": "devboard/client/src/components/Task/TaskModal.jsx#TaskModal"
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
      "target": "devboard/client/src/pages/Dashboard.jsx#Dashboard"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/context/BoardContext.jsx#BoardProvider"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/server/routes/tasks.js:7-127"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/server/models/Task.js#taskSchema"
    }
  ]
}
---

# Archive filtered completed tasks by deletion

## Trigger

The Developer confirms removing the filtered Done tasks.

## Outcome

Matching Done tasks in the current search/tag-filtered collection are permanently removed.

## Edge cases

- Canceled confirmation removes nothing.
- Done tasks outside the current search/tag-filtered collection remain.
- Archive has no recovery or archived lifecycle state.
- Existing local pin records are not automatically cleared.

## Card lifetime

This case removes paused mounted card trackers. A running tracker also ends on card unmount; deletion is not broadcast to other connected clients.
