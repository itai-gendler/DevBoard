---
{
  "id": "devboard",
  "summary": "A developer Kanban board for tasks, code snippets, issue references, exports and focus timing.",
  "category": "developer-tools",
  "authors": [
    {
      "name": "DevBoard Contributors"
    }
  ],
  "license": "MIT",
  "languages": [
    "en"
  ],
  "limitations": [
    "Task status is always Backlog, In Progress, Review or Done; columns added in the browser do not extend it.",
    "Demo Mode keeps tasks only in the open browser session, without server storage, history or live updates.",
    "Issue references link tasks to GitHub issues; task changes are never sent back to GitHub.",
    "Board preferences, task templates and focus sessions stay in the browser, apart from account tasks."
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/App.jsx#PrivateRoute"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/pages/Login.jsx#handleSubmit"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/pages/Dashboard.jsx#Dashboard"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/components/Task/TaskModal.jsx#TaskModal"
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

# DevBoard

Developers organize task work on a Kanban board, keep code and issue references with tasks, export task information, and use focus and elapsed-time tools. Account-backed work and public Demo Mode have distinct persistence and acceptance.

Notes are shared task content despite the Private Notes label. Archive removes the filtered completed tasks permanently. Issue references do not synchronize task changes to GitHub. Browser-local preferences, templates and timing are separate from server task persistence.

## Intent

Give developers a task board built for their own work rather than for project managers, keeping code, issue references and focus time with each task so they need not leave their workflow.
