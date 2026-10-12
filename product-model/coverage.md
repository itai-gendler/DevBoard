---
{
  "scope": "Current account-access, demo and connected web board source and its wired persistence, timing and outbound dependency handlers.",
  "method": "Static entry-point-to-outcome inspection of pinned source and repository documentation.",
  "covered": [
    {
      "description": "Web routing, account entry, cached context and task-resolution code, bounded to mapped web flows.",
      "paths": [
        "devboard/client/src/App.jsx",
        "devboard/client/src/pages/",
        "devboard/client/src/context/"
      ]
    },
    {
      "description": "Kanban operations, task forms, code, copying, exports and local preference code.",
      "paths": [
        "devboard/client/src/components/Board/",
        "devboard/client/src/components/Task/"
      ]
    },
    {
      "description": "Timer, activity-summary and outbound generation/project-count hooks and components.",
      "paths": [
        "devboard/client/src/components/Pomodoro/",
        "devboard/client/src/components/Heatmap/",
        "devboard/client/src/hooks/"
      ]
    },
    {
      "description": "Visit stamps and relative-time derivation utilities.",
      "paths": [
        "devboard/client/src/utils/lastVisit.js",
        "devboard/client/src/utils/timeAgo.js"
      ]
    },
    {
      "description": "Account/task model declarations, wired auth/task/AI requests and identity middleware.",
      "paths": [
        "devboard/server/models/",
        "devboard/server/routes/auth.js",
        "devboard/server/routes/tasks.js",
        "devboard/server/routes/ai.js",
        "devboard/server/middleware/auth.js"
      ]
    },
    {
      "description": "Handler mounting and update broadcasts supporting the web receiver.",
      "paths": [
        "devboard/server/index.js",
        "devboard/server/config/constants.js"
      ]
    }
  ],
  "exclusions": [
    {
      "description": "Visual styling, icon/avatar coloring, browser images and screenshot assets.",
      "paths": [
        "devboard/client/src/index.css",
        "devboard/client/src/components/common/",
        "devboard/client/src/utils/avatarColor.js",
        "devboard/client/public/",
        "devboard/docs/"
      ]
    },
    {
      "description": "Build and dependency metadata, bootstrap and style-tool configuration.",
      "paths": [
        "package-lock.json",
        "devboard/package.json",
        "devboard/package-lock.json",
        "devboard/client/package.json",
        "devboard/client/package-lock.json",
        "devboard/server/package.json",
        "devboard/server/package-lock.json",
        "devboard/client/vite.config.js",
        "devboard/client/postcss.config.js",
        "devboard/client/tailwind.config.js",
        "devboard/client/index.html",
        "devboard/client/src/main.jsx"
      ]
    },
    {
      "description": "Contribution/changelog scaffolding and operational request-timing code.",
      "paths": [
        "CONTRIBUTING.md",
        "CHANGELOG.md",
        "devboard/CONTRIBUTING.md",
        "devboard/server/middleware/responseTime.js"
      ]
    }
  ],
  "unmapped": [
    {
      "description": "Inspected GitHub issue fetch/import handlers without a supported independent inbound contract.",
      "paths": [
        "devboard/server/routes/github.js"
      ]
    },
    {
      "description": "Unwired logout-all and standalone snippet-append/count-increment functions and endpoints.",
      "paths": [
        "devboard/server/routes/auth.js",
        "devboard/server/routes/tasks.js",
        "devboard/client/src/context/BoardContext.jsx"
      ]
    },
    {
      "description": "API-only assignment and raw history editing, project/reaction fields, and independent profile lifecycle.",
      "paths": [
        "devboard/server/models/",
        "devboard/server/routes/tasks.js",
        "devboard/server/routes/auth.js",
        "devboard/client/src/components/Task/TaskModal.jsx"
      ]
    },
    {
      "description": "Independent HTTP/socket consumer contracts, health/root diagnostics, quotas and unrendered online counts.",
      "paths": [
        "devboard/server/index.js",
        "devboard/client/src/context/BoardContext.jsx"
      ]
    },
    {
      "description": "Unwired install/fullscreen/print control code.",
      "paths": [
        "devboard/client/src/pages/Dashboard.jsx"
      ]
    }
  ],
  "limitations": [
    {
      "description": "Configured external-service and deployment outcomes are not established by the inspected adapters and example environment values.",
      "paths": [
        "devboard/server/routes/ai.js",
        "devboard/server/routes/github.js",
        "devboard/server/index.js",
        "devboard/.env.example",
        "devboard/server/.env.example"
      ]
    }
  ]
}
---

# Coverage


