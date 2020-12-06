# Find profile's username history
This endpoint allows users to find the username history of a Minecraft profile. There are two endpoints that do this task. Both are identical in their function, however the URLs are slightly different.

### Request
- **Method:** `GET`
- **Endpoint 1:** `/user/profiles/:uuid/names`
- **Endpoint 2:** `/user/profile/:uuid/names`
- **Full URL 1:** `https://api.mojang.com/user/profiles/:uuid/names`
- **Full URL 1:** `https://api.mojang.com/user/profile/:uuid/names`

The only URL parameter required is `uuid`, the UUID of the profile you wish to find the username history of.

### Response
**200: OK**

A valid user exists with this UUID, and the response is their name history in JSON format. 

The `changedToAt` key's value in each element of the array is in Unix epoch time format, in milliseconds. If there is no `changedToAt` key, that username was the account's first username. 

Typically, accounts with zero username history and whose usernames have been on no other accounts are called "prename accounts". A sample response is below:

```json
[
  {
    "name" : "Blaschki" // the account's first username
  },
  {
    "name" : "SuperSimon26",
    "changedToAt" : 1532898007000
  },
  {
    "name" : "UNHhhhhh",
    "changedToAt" : 1564349304000
  },
  {
    "name" : "FireWire",
    "changedToAt" : 1604340219000
  }
]
```

**204: No Content**

There is no response for this error. If you encounter this error, the UUID you have provided has either never been on a profile or has been on a profile that is hard-deleted.

**400: Bad Request**

If you encounter this error, you have supplied a UUID that is invalid (not valid UUIDv4).

```json
{
  "error" : "BadRequestException",
  "errorMessage" : "Invalid ID size: faketext"
}
```

**Note:** There seems to be virtually no ratelimit on this endpoint. Update this information if it is false.
