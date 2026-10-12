---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer submits email and password",
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
      "text": "The Product checks the Account credential",
      "kind": "product",
      "entities": [
        {
          "entity": "account",
          "effect": "reads",
          "facts": [
            "Email",
            "Password"
          ]
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::public::sign-in"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product establishes the browser credential and carries the Developer toward the connected board",
      "kind": "product",
      "entities": [
        {
          "entity": "account",
          "effect": "reads",
          "facts": [
            "Name",
            "Email"
          ]
        }
      ],
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
      "target": "devboard/server/models/User.js#userSchema"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/server/routes/auth.js:6-57"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/server/middleware/auth.js#protect"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/server/routes/auth.js#generateToken"
    }
  ]
}
---

# Sign in with matching credentials

## Trigger

The Developer submits Email and Password for sign-in.

## Outcome

Matching credentials establish connected browser access and the board destination. The previously requested task link is not restored.

## Edge cases

- The client trims email before submission; Account email is stored in lowercase.
- The returned credential has a thirty-day expiry; cached tasks are not purged before fetching.
