---
{
  "entities": [
    {
      "entity": "task",
      "collects": [
        "Title",
        "Description",
        "Notes",
        "Status",
        "Priority",
        "Tags",
        "Issue URL",
        "Issue number",
        "Due date",
        "Estimate"
      ]
    },
    {
      "entity": "code-snippet",
      "collects": [
        "Language",
        "Code"
      ]
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

# New Task

The task creation process takes content, initial column and optional new code. Generated descriptions and entered code remain unsaved until task creation succeeds. Attempted dependency selections are sent by the form but discarded by connected persistence; they are not a kept Task fact.
