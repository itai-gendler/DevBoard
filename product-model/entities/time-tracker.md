---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/components/Board/TaskCard.jsx#TaskCard"
    }
  ]
}
---

# Time tracker

An elapsed-time tracker scoped to one mounted task card.

## Information kept

- **Elapsed time** — Seconds tracked by this card instance.

## States

### Paused

Elapsed time does not advance.

### Running

Elapsed time advances while the card remains mounted.
