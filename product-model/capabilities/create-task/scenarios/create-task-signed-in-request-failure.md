---
{
  "kind": "edge",
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
      "text": "The creation request fails without a confirmed successful response",
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

# Fail the task-creation request

## Trigger

The Developer opens New Task, supplies content and optional code, and chooses Save.

## Outcome

No creation is confirmed to the client; failure is logged and ordinary Save can remain busy.

## Edge cases

- A rejected request does not promise uniform visible feedback or retry recovery.
