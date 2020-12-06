# Username to UUID (GET)
This endpoint allows users to supply a username to be checked and get its UUID if the username resolves to a valid Minecraft profile.

There are two endpoints that do this task. Both are the same in function, however the URLs are different.

### Request
- **Method:** `GET`
- **Endpoint 1:** `/users/profiles/minecraft/:username`
- **Endpoint 2:** `/user/profile/agent/minecraft/name/:username`
- **Full URL 1:** `https://api.mojang.com/users/profiles/minecraft/:username`
- **Full URL 2:** `https://api.mojang.com/user/profile/agent/minecraft/name/:username`

The only URL parameter that is needed is `username`, the username that you want to look up.

### Response
**200: OK**

A valid UUID was found for the supplied username. Sample response:

```json
{
  "name" : "lukethehacker23", // account username
  "id" : "cdb5aee80f904fdda63ba16d38cd6b3b" // UUID of account
}
```

**204: No Content**

There is no response for this error. If you encounter this error, the username you have provided has either never been on a profile, is currently dropping to the public (on cooldown), or has been on a profile that is deleted (either hard-deleted or pseudo-hard-deleted).

**400: Bad Request**

Most likely, the reason you are getting this error is because you've supplied an invalid username as the `username` URL parameter.


```json
// invalid length
{
  "error" : "BadRequestException",
  "errorMessage" : "obviouslyanamethatistoolongforminecraft is invalid"
}

// invalid character
{
  "error" : "BadRequestException",
  "errorMessage" : "& is invalid"
}
```

**405: Method Not Allowed**

You did not make the request a GET request.

```json
{
  "error" : "Method Not Allowed",
  "errorMessage" : "The method specified in the request is not allowed for the resource identified by the request URI"
}
```

**429: Too Many Requests**

If you get this error, you have sent too many requests and must wait at least 30 seconds before sending another.

```json
{
  "error" : "TooManyRequestsException",
  "errorMessage" : "The client has sent too many requests within a certain amount of time"
}
```
