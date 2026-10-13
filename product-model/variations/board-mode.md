---
{
  "kind": "configuration",
  "of": "entity",
  "settings": [
    {
      "entity": "developer",
      "fact": "Browser identity"
    }
  ],
  "takesEffect": "When the browser identity is set: on a fresh visit, when the Developer chooses Explore Demo Mode, or when sign-in or account creation succeeds.",
  "stability": "Holds until sign-out or until another identity replaces it. Demo Task changes live only in the open browser session and are lost on reload or sign-out; tasks already loaded stay in view when switching into Demo Mode. Account Tasks stay on the server.",
  "alternatives": [
    {
      "id": "demo-task",
      "selectedWhen": "The browser identity carries the demo credential. A browser with no readable stored identity starts this way."
    },
    {
      "id": "task",
      "selectedWhen": "The browser identity carries an account credential issued at sign-in or account creation."
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/context/BoardContext.jsx#BoardProvider"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/pages/Login.jsx:90-99"
    }
  ]
}
---

# Demo Mode or account board

DevBoard supports two ways to keep board tasks: Demo Mode keeps them in the browser only, with no server, live updates or history, and an account keeps them on the server with history and live updates for other viewers.
