# Check if security questions are needed
This endpoint will tell the user if they need to answer security questions or if they are not needed (is the location verified or not?)

### Request
- **Method:** `GET`
- **Endpoint:** `/user/security/location`
- **Full URL:** `https://api.mojang.com/user/security/location`
- **Headers:**
    - `Authorization: Bearer [JWT/auth token here]`

### Response
**204: No Content**

No response for this status code. No security questions are needed, feel free to use any endpoints that require authorization without the need to answer security questions or authorize your location / IP address.

**401: Unauthorized**

You provided an invalid Bearer token or neglected to fill in the `Authorization` header entirely.

```json
{
   "error" : "Unauthorized",
   "errorMessage" : "The request requires user authentication"
}
```

**403: Forbidden**

Security questions are needed. You must use the "Get security questions" endpoint, then submit the answers using the "Send security answers" endpoint in order to use endpoints that require an authorized location / IP address.

```json
{
   "error" : "ForbiddenOperationException",
   "errorMessage" : "Current IP is not secured"
}
```
