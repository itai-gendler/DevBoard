---
{
  "kind": "primary",
  "routes": {
    "web": "New Task",
    "edit": "Edit Task"
  },
  "steps": [
    {
      "text": "The Developer requests a description for the supplied title",
      "kind": "actor",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::new-task"
        },
        "edit": {
          "place": "devboard-web::signed-in::edit-task"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product requests description text from Gemini",
      "kind": "product",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::new-task"
        },
        "edit": {
          "place": "devboard-web::signed-in::edit-task"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product fills the current unsaved description input with returned text",
      "kind": "product",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::new-task"
        },
        "edit": {
          "place": "devboard-web::signed-in::edit-task"
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
      "target": "devboard/server/routes/ai.js:7-95"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/hooks/useSuggestTags.jsx#useSuggestTags"
    }
  ]
}
---

# Fill an unsaved AI description

## Trigger

The Developer requests AI description text from the current title input.

## Outcome

Generated text fills the unsaved form without changing a stored task. Saving the form is the acceptance.

## Edge cases

- The prompt requests concise two-to-three-sentence text but does not establish a guaranteed sentence count.
- Programmatic filling does not impose the typed-description maxlength budget on returned text.
- An empty returned description can still fill the input; no kept AI draft is created.
