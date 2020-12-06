# Check your account's capes
This endpoint allows an authenticated user to view information about their owned Minecraft capes.

**Note:** This endpoint is now deprecated. Use the "View profile information" endpoint instead.

### Request
- **Method:** `GET`
- **Endpoint:** `/user/profile/:uuid/cape`
- **Full URL:** `https://api.mojang.com/user/profile/:uuid/cape`
- **Headers:**
    - `Authorization: Bearer [JWT/auth token here]`

The only URL parameter here is `uuid`, the UUID tied to your Minecraft profile & Bearer token.

### Response
**200: OK**

No errors occurred while fetching cape information. An empty array (`[]`) is returned if the account has no capes. Sample response below:

```json
// if account has capes
[
  {
    "id": "9aa1d1dc61fb47ab9b62e79303fb8922", // internal cape identifier
    "alias": "Minecon2013", // human-readable cape name
    "type": "CAPE", // "SKIN" for a skin
    "url": "http://textures.minecraft.net/texture/153b1a0dfcbae953cdeb6f2c2bf6bf79943239b1372780da44bcbb29273131da", // texture URL
    "visible": true, // is the cape visible?
    "profileId": "c3d8e16622234b6bb6bcccf7907fb35a", // UUID of account
    "textureId": "153b1a0dfcbae953cdeb6f2c2bf6bf79943239b1372780da44bcbb29273131da", // texture id
    "selected": true, // is the cape currently enabled on the profile?
    "deleted": false, // has the cape been deleted?
    "version": 2 // implies a v1... not sure
  }
]

// if no capes
[]
```

**401: Unauthorized**

This error occurs when you either haven't answered your security questions, or when you've passed an invalid or expired Bearer token in the `Authorization` header.

```json
{
  "error" : "UnauthorizedOperationException",
  "errorMessage" : "User not authenticated"
}
```

**403: Forbidden**

When getting this error, you have most likely tried to view cape information tied to a UUID of a profile that is not linked to your Bearer token.

```json
{
  "error" : "ForbiddenOperationException",
  "errorMessage" : "Invalid profile id or access token."
}
```
