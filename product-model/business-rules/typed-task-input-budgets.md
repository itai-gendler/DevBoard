---
{
  "appliesTo": [
    {
      "type": "context",
      "context": {
        "place": "devboard-web::public::new-task"
      }
    },
    {
      "type": "context",
      "context": {
        "place": "devboard-web::public::edit-task"
      }
    },
    {
      "type": "context",
      "context": {
        "place": "devboard-web::signed-in::new-task"
      }
    },
    {
      "type": "context",
      "context": {
        "place": "devboard-web::signed-in::edit-task"
      }
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/components/Task/TaskModal.jsx#TaskModal"
    }
  ]
}
---

# Typed task inputs observe their field budgets

Manual title input is limited to 100 characters, description to 500, and the entire comma-separated tag-list input to 120. AI filling, suggestion selection and direct requests are not universal applications of those manual-input limits.
