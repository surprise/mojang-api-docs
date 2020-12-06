# Get security questions
This endpoint fetches the list of security questions you must answer on your account.

### Request
- **Method:** `GET`
- **Endpoint:** `/user/security/challenges`
- **Full URL:** `https://api.mojang.com/user/security/challenges`
- **Headers:**
    - `Authorization: Bearer [JWT/auth token here]`

### Response
**200: OK**

Success retrieving security questions. If the returned response is `[]` (empty array), there are no challenges on the authenticated account, and therefore the account has no security questions. Otherwise, the security questions are returned.

```json
// when there are security questions
[
   {
      "answer": {
         "id": 123 // the ID of the answer, needed when answering questions
      },
      "question": {
         "id": 1, // number of security question in the pre-defined list of 39
         "question": "What is your favorite pet's name?"
      }
   },
   {
      "answer": {
         "id": 456 // the ID of the answer, needed when answering questions
      },
      "question": {
         "id": 26, // number of security question in the pre-defined list of 39
         "question": "What was your first gaming console?"
      }
   },
   {
      "answer": {
         "id": 789 // the ID of the answer, needed when answering questions
      },
      "question": {
         "id": 34, // number of security question in the pre-defined list of 39
         "question": "What is your favorite ice cream flavor?"
      }
   }
]

// no security questions on account
[]
```

**401: Unauthorized**

You provided an invalid Bearer token or neglected to fill in the `Authorization` header entirely.

```json
{
   "error" : "Unauthorized",
   "errorMessage" : "The request requires user authentication"
}
```
