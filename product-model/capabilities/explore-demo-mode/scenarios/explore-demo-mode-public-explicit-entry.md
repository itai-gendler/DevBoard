---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer chooses Explore Demo Mode",
      "kind": "actor",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::public::sign-in"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product initializes the mock-token browser context",
      "kind": "product",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::public::sign-in"
        }
      },
      "actor": "developer"
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
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/context/BoardContext.jsx#BoardProvider"
    }
  ]
}
---

# Enter Demo Mode explicitly

## Trigger

The Developer chooses Explore Demo Mode.

## Outcome

The demo board is the destination. The explicit profile is retained in browser storage; existing task data is not first cleared.

## Edge cases

- The explicit profile uses a different identifier field from the local viewer routine.
- Demo fixture profiles are shipped content, not registered identities.
