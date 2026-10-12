---
{
  "kind": "edge",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer confirms removing two Done Task entries in the current filtered collection",
      "kind": "actor",
      "entities": [
        {
          "entity": "task",
          "as": "saved",
          "effect": "reads",
          "facts": [
            "Title",
            "Status"
          ]
        },
        {
          "entity": "task",
          "as": "failed",
          "effect": "reads",
          "facts": [
            "Title",
            "Status"
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
      "text": "The Product removes a successfully deleted task and its contained Code Snippet and histories; their paused mounted Time tracker instances end when the local cards unmount",
      "kind": "product",
      "entities": [
        {
          "entity": "task",
          "effect": "removes",
          "from": "Done",
          "as": "saved"
        },
        {
          "entity": "code-snippet",
          "effect": "removes",
          "with": "saved",
          "as": "saved-code-snippet"
        },
        {
          "entity": "recent-activity",
          "effect": "removes",
          "with": "saved",
          "as": "saved-recent-activity"
        },
        {
          "entity": "assignee-history",
          "effect": "removes",
          "with": "saved",
          "as": "saved-assignee-history"
        },
        {
          "entity": "time-tracker",
          "effect": "removes",
          "as": "saved-time-tracker",
          "from": "Paused",
          "with": "saved"
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
      "text": "The other deletion fails and its Task remains in the local collection",
      "kind": "condition",
      "entities": [
        {
          "entity": "task",
          "as": "failed",
          "effect": "reads",
          "facts": [
            "Status"
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

# Retain successful archive deletions despite another failure

## Trigger

The Developer confirms removing the filtered Done tasks.

## Outcome

Successful deletions remain removed. The archive does not roll back completed deletions.

## Card lifetime

This case removes paused mounted card trackers. A running tracker also ends on card unmount; deletion is not broadcast to other connected clients.
