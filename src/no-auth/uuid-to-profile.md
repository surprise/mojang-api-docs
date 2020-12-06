# UUID to user profile (skins, capes, etc.)
This endpoint allows users to supply a UUID to be checked and get its profile information (username, legacy status, skin, and cape), if it resolves to a valid Minecraft profile.

Keep in mind that this endpoint is not on the normal Mojang API subdomain, instead it is located on `sessionserver.mojang.com`.

### Request
- **Method:** `GET`
- **Endpoint:** `/session/minecraft/profile/:uuid`
- **Full URL:** `https://sessionserver.mojang.com/session/minecraft/profile/:uuid`

The only URL parameter that is needed is `uuid`, the UUID that you want to look up.

### Response
**200: OK**

A valid Minecraft profile was found for the supplied UUID. Sample response below:

```json
{
  "id" : "f1bfcbddc68b49bfaac9fb9d8ce5293d", // UUID of account
  "name" : "123lmfao4", // account username
  "properties" : [ {
    "name" : "textures",
    "value" : "ewogICJ0aW1lc3RhbXAiIDogMTYwNzAwNDI0NTk2OCwKICAicHJvZmlsZUlkIiA6ICJmMWJmY2JkZGM2OGI0OWJmYWFjOWZiOWQ4Y2U1MjkzZCIsCiAgInByb2ZpbGVOYW1lIiA6ICIxMjNsbWZhbzQiLAogICJ0ZXh0dXJlcyIgOiB7CiAgICAiU0tJTiIgOiB7CiAgICAgICJ1cmwiIDogImh0dHA6Ly90ZXh0dXJlcy5taW5lY3JhZnQubmV0L3RleHR1cmUvZTM1ZjNhOGRmOTY5YjU2YjM2ZjlhYTYwYTczNmEyZjkwNjFkZTRjY2YwZmU5NjU3ZDZjOWJjMDJkNzdiZmQ3ZSIsCiAgICAgICJtZXRhZGF0YSIgOiB7CiAgICAgICAgIm1vZGVsIiA6ICJzbGltIgogICAgICB9CiAgICB9CiAgfQp9" // base64-encoded texture information
  } ],
  "legacy" : true // will only appear if profile is legacy / unmigrated (2010-2012). if profile is migrated this just won't show up
}
```

The base64-encoded texture information, when decoded, is another bit of JSON. Sample response below (added cape information from another profile, `123lmfao4` does not have a cape):

```json
{
  "timestamp" : 1607004245968, // timestamp when you sent the request
  "profileId" : "f1bfcbddc68b49bfaac9fb9d8ce5293d", // UUID of account
  "profileName" : "123lmfao4", // account username
  "textures" : {
    "SKIN" : {
      "url" : "http://textures.minecraft.net/texture/e35f3a8df969b56b36f9aa60a736a2f9061de4ccf0fe9657d6c9bc02d77bfd7e", // skin URL
      "metadata" : {
        "model" : "slim" // alex (slim) or steve (classic)?
      }
    },
    "CAPE" : { // will not show up if account doesn't have a cape
      "url" : "http://textures.minecraft.net/texture/153b1a0dfcbae953cdeb6f2c2bf6bf79943239b1372780da44bcbb29273131da" // cape URL
    }
  }
}
```

**204: No Content**

There is no response for this error. If you encounter this error, the UUID you have provided has either never been on a profile or has been on a profile that is hard-deleted.

**400: Bad Request**

When getting this error, you most likely have supplied an invalid UUID (invalid length).

```json
// invalid length
{
  "error" : "Bad Request",
  "path" : "/session/minecraft/profile/invalid_uuid"
}

// invalid characters
{
  "error" : "Bad Request",
  "path" : "/session/minecraft/profile/3126ba4c6uud424c877d1347fa974d23"
}
```
