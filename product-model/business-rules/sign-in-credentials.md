---
{
  "appliesTo": [
    {
      "type": "capability-scenario",
      "id": "sign-in-public-accepted",
      "contexts": [
        {
          "place": "devboard-web::public"
        }
      ]
    },
    {
      "type": "capability-scenario",
      "id": "sign-in-public-invalid-form",
      "contexts": [
        {
          "place": "devboard-web::public"
        }
      ]
    },
    {
      "type": "capability-scenario",
      "id": "sign-in-public-credentials-rejected",
      "contexts": [
        {
          "place": "devboard-web::public"
        }
      ]
    },
    {
      "type": "capability-scenario",
      "id": "sign-in-public-service-failure",
      "contexts": [
        {
          "place": "devboard-web::public"
        }
      ]
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
    }
  ]
}
---

# Sign-in checks matching credentials and client form validity

The client requires email with an at-sign and a password of at least six characters, then trims email before submission. The lookup and password comparison must match a registered Account to establish the returned credential. Account email is stored in lowercase. Wrong credentials and service failure have distinct outcomes.
