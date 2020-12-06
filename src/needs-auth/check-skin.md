# Check your account's skin (old)
This endpoint allows an authenticated user to view information about their applied Minecraft skin.

**Note:** This endpoint is now deprecated. Use the "View profile information" endpoint instead.

### Request
- **Method:** `GET`
- **Endpoint:** `/user/profile/:uuid/skins`
- **Full URL:** `https://api.mojang.com/user/profile/:uuid/skins`
- **Headers:**
    - `Authorization: Bearer [JWT/auth token here]`

The only URL parameter here is `uuid`, the UUID tied to your Minecraft profile & Bearer token.

### Response
**200: OK**

No errors occurred while fetching skin information. Sample response below:

```json
[
  {
    "id": "94607f47c63c4356b1d8cb57ad2342e0", // internal skin identifier
    "type": "SKIN", // "CAPE" for a cape
    "url": "http://textures.minecraft.net/texture/3b60a1f6d562f52aaebbf1434f1de147933a3affe0e764fa49ea057536623cd3", // texture URL
    "visible": true, // is the skin visible?
    "profileId": "f933f85fc46046038e5f579ee1c919c5", // UUID of account
    "textureId": "3b60a1f6d562f52aaebbf1434f1de147933a3affe0e764fa49ea057536623cd3", // texture id
    "selected": true, // is the skin currently enabled on the profile?
    "deleted": false, // has the skin been deleted?
    "metadata": {
      "model": "slim" // alex (slim) or steve (classic) ?
    },
    "version": 2 // implies a v1... not sure
  }
]
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

When getting this error, you have most likely tried to view skin information tied to a UUID of a profile that is not linked to your Bearer token.

```json
{
  "error" : "ForbiddenOperationException",
  "errorMessage" : "Invalid profile id or access token."
}
```
