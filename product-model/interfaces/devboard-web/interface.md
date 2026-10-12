---
{
  "type": "web",
  "actors": [
    "developer"
  ],
  "languages": [
    "en"
  ],
  "entryPoints": [
    {
      "web": "/login"
    },
    {
      "web": "/"
    },
    {
      "web": "/task/:id"
    }
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
    }
  ]
}
---

# DevBoard web

The Developer uses the web board, account-access process and linked task working context.
