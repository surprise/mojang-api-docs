# UUID to username
This endpoint allows users to supply a UUID to be checked and get its username if the UUID resolves to a valid Minecraft profile.

### Request
- **Method:** `GET`
- **Endpoint:** `/user/profile/:uuid`
- **Full URL:** `https://api.mojang.com/user/profile/:uuid`

The only URL parameter that is needed is `uuid`, the UUID that you want to look up.

### Response
**200: OK**

A valid username was found for the supplied UUID. Sample response:

```json
{
  "name" : "lukethehacker23", // account username
  "id" : "cdb5aee80f904fdda63ba16d38cd6b3b" // UUID of account
}
```

**204: No Content**

There is no response for this error. If you encounter this error, the UUID you have provided has either never been on a profile or has been on a profile that is hard-deleted.

**400: Bad Request**

Most likely, the reason you are getting this error is because you've supplied an invalid UUID as the `uuid` URL parameter.


```json
// invalid length
{
  "error" : "BadRequestException",
  "errorMessage" : "Invalid ID size: obviouslyanidthatistoolongforminecraft"
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

