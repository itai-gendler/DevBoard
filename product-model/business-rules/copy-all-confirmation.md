---
{
  "appliesTo": [
    {
      "type": "capability-scenario",
      "id": "copy-task-information-public-all-code",
      "contexts": [
        {
          "place": "devboard-web::public"
        }
      ]
    },
    {
      "type": "capability-scenario",
      "id": "copy-task-information-public-all-code-copy-refused",
      "contexts": [
        {
          "place": "devboard-web::public"
        }
      ]
    },
    {
      "type": "capability-scenario",
      "id": "copy-task-information-signed-in-all-code",
      "contexts": [
        {
          "place": "devboard-web::signed-in"
        }
      ]
    },
    {
      "type": "capability-scenario",
      "id": "copy-task-information-signed-in-all-code-copy-refused",
      "contexts": [
        {
          "place": "devboard-web::signed-in"
        }
      ]
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
      "target": "devboard/client/src/components/Board/TaskCard.jsx#TaskCard"
    }
  ]
}
---

# All-code success follows clipboard acceptance

The all-code action awaits clipboard writing before reporting success and presents failure on refusal. Title, selected-code, JSON and link actions do not share this confirmation guarantee.
