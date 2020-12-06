# Change your account's username
This endpoint allows a user with a Minecraft profile to change their account's username.

### Request
- **Method:** `PUT`
- **Endpoint:** `/minecraft/profile/name/:username`
- **Full URL:** `https://api.minecraftservices.com/minecraft/profile/name/:username`
- **Headers:**
    - `Authorization: Bearer [JWT/auth token here]`

The only URL parameter is `username`, your desired username.

### Response
**200: OK**

You have successfully changed your account's username!

```json
// just returns normal user profile response
{
  "id" : "31e0ccbef5fa4eb988592f30516f65fe",
  "name" : "newname34234",
  "skins" : [ {
    "id" : "c97f6fea-6ca8-4bf0-bdae-b7cf91fb089c",
    "state" : "ACTIVE",
    "url" : "http://textures.minecraft.net/texture/3b60a1f6d562f52aaebbf1434f1de147933a3affe0e764fa49ea057536623cd3",
    "variant" : "SLIM"
  } ],
  "capes" : [ ]
}
```

**400: Bad Request**

This status code is returned when an error occurred when changing your username. Below is a list of the possible errors:

```json
// trying to change to a name of invalid length
{
  "path" : "/minecraft/profile/name/1",
  "errorType" : "CONSTRAINT_VIOLATION",
  "error" : "CONSTRAINT_VIOLATION",
  "errorMessage" : "changeProfileName.profileName: Invalid profile name, changeProfileName.profileName: size must be between 3 and 16",
  "developerMessage" : "changeProfileName.profileName: Invalid profile name, changeProfileName.profileName: size must be between 3 and 16"
}

// trying to change to a name with invalid characters
{
  "path" : "/minecraft/profile/name/%%%%%",
  "errorType" : "CONSTRAINT_VIOLATION",
  "error" : "CONSTRAINT_VIOLATION",
  "errorMessage" : "changeProfileName.profileName: Invalid profile name",
  "developerMessage" : "changeProfileName.profileName: Invalid profile name"
}
```

If interested, invalid length validation takes priority over invalid name violation, it seems.

**401: Unauthorized**

You have not provided a valid JWT / auth token, or you have neglected to provide the `Authorization` header at all.

```json
{
  "path" : "/minecraft/profile/name/:username",
  "errorType" : "UnauthorizedOperationException",
  "error" : "UnauthorizedOperationException",
  "errorMessage" : "Unauthorized",
  "developerMessage" : "Unauthorized"
}
```

**403: Forbidden**

If this error occurs, you are either trying to change the username of an account that has already changed its username in the past 30 days, **OR** you are trying to change the username of your account to a name that has already been taken or is still on cooldown.

```json
{
  "path" : "/minecraft/profile/name/:username",
  "errorType" : "FORBIDDEN",
  "error" : "FORBIDDEN"
}
```

**429: Too Many Requests**

If you have sent too many requests in a specific amount of time (3 requests every 60 seconds seems to be the limit), this error will appear.

```json
{
  "path" : "/minecraft/profile/name/:username",
  "errorType" : "TooManyRequestsException",
  "error" : "TooManyRequestsException",
  "errorMessage" : "The client has sent too many requests within a certain amount of time",
  "developerMessage" : "The client has sent too many requests within a certain amount of time"
}
```

**500: Internal Server Error**

If this status code is returned, you are most likely trying to change the username of an account that has security questions enabled, which you have not answered. Other issues could cause this error as well, for example if the API is being overloaded.

```json
{
  "path" : "/minecraft/profile/name/:username",
  "errorType" : "EXTERNAL_API_ERROR",
  "error" : "EXTERNAL_API_ERROR",
  "errorMessage" : "",
  "developerMessage" : ""
}
```
