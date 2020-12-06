# Send security answers
This endpoint allows an authenticated user to verify their location by answering their security questions.

This endpoint was the cause of the first [NFA to FA exploit](https://www.youtube.com/watch?v=KvF0Bvo1GsY) from early 2020.

### Request
- **Method:** `POST`
- **Endpoint:** `/user/security/location`
- **Full URL:** `https://api.mojang.com/user/security/location`
- **Headers:**
    - `Authorization: Bearer [JWT/auth token here]`

The POST body must be similar to:

```json
[
  {
    "id": 123, // answer ID
    "answer": "foo"
  },
  {
    "id": 456, // answer ID
    "answer": "bar"
  },
  {
    "id": 789, // answer ID
    "answer": "baz"
  }
]
```

### Response
**204: No Content**

No response for this status code. You have successfully authorized your location / IP address.

**400: Bad Request**

When you get this response, most likely you've submitted the same answer ID and answer multiple times. This is what the old NFA to FA exploit was based off of.

```json
{
   "error" : "IllegalArgumentException",
   "errorMessage" : "3 answers required to secure location"
}
```

**403: Forbidden**

When you get this response, one of the answers you submitted wasn't correct.

```json
{
   "error" : "ForbiddenOperationException",
   "errorMessage" : "At least one answer was incorrect"
}
```
