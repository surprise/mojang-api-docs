# Name change eligibility
This endpoint allows a user with a Minecraft profile to check if they are able to change their username (30 day cooldown).

This endpoint also allows a user to view the date their account was made premium, this includes legacy / unmigrated users.

### Request
- **Method:** `GET`
- **Endpoint:** `/minecraft/profile/namechange`
- **Full URL:** `https://api.minecraftservices.com/minecraft/profile/namechange`
- **Headers:**
    - `Authorization: Bearer [JWT/auth token here]`

### Response
**200: OK**

This seems to be the only status code returned, save for 401 and 429.

```json
{
  "changedAt" : "2020-12-02T03:11:01Z", // the time you last changed your name at
  "createdAt" : "2020-06-08T05:44:42Z", // creation date of account
  "nameChangeAllowed" : false // true when you are able to name change
}
```

**401: Unauthorized**

You have not provided a valid JWT / auth token, or you have neglected to provide the `Authorization` header at all.

```json
{
  "path" : "/minecraft/profile/namechange",
  "errorType" : "UnauthorizedOperationException",
  "error" : "UnauthorizedOperationException",
  "errorMessage" : "Unauthorized",
  "developerMessage" : "Unauthorized"
}
```

**429: Too Many Requests**

If you have sent too many requests in a specific amount of time, this error will appear.

```json
{
  "path" : "/minecraft/profile/namechange",
  "errorType" : "TooManyRequestsException",
  "error" : "TooManyRequestsException",
  "errorMessage" : "The client has sent too many requests within a certain amount of time",
  "developerMessage" : "The client has sent too many requests within a certain amount of time"
}
```
