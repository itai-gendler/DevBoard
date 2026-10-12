---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/hooks/usePomodoro.js#usePomodoro"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/pages/Dashboard.jsx#handleSessionComplete"
    }
  ]
}
---

# Pomodoro timer

A transient work/break timer for the mounted board with browser-remembered completed-session count.

## Information kept

- **Phase** — Work or Break.
- **Remaining time** — Seconds remaining in the current phase.
- **Completed sessions** — The current completed-work-session count.
- **Remembered sessions** — The completed count last retained in browser storage.
- **Attached task** — The task selected on the board at the time the timer observes its attachment, if any.

## States

### Stopped

The countdown is not advancing.

### Running

The countdown advances toward phase expiry.
