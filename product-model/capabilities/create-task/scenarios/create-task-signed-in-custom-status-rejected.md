---
{
  "kind": "validation",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer submits the new content and selected initial column",
      "kind": "actor",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::new-task"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The submitted local column name is outside the stored status vocabulary",
      "kind": "condition",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::new-task"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product keeps the creation process open without a confirmed new entry",
      "kind": "product",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::new-task"
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

# Reject unsupported connected initial status

## Trigger

The Developer opens New Task, supplies content and optional code, and chooses Save.

## Outcome

Server validation rejects the unsupported status; the custom browser column still exists.

## Edge cases

- A rejected request does not promise uniform visible feedback or retry recovery.
