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

# Normal task saving rejects blank or currently duplicated titles

Normal Save requires a nonblank trimmed title and refuses another currently loaded task with the same trimmed case-insensitive title, excluding the selected identifier. Duplication does not use this duplicate-title refusal. This is a loaded-collection form check, not a server-wide uniqueness promise.
