# Redeem a giftcode / voucher
This endpoint allows an authenticated user on a Microsoft account to redeem a product voucher, which could be a gift code, prepaid card, etc.

Keep in mind that after successfully redeeming the voucher, you must then create a Minecraft profile (Section 3.3). If you do not, you will just have a copy of the game with no profile, waiting for you to choose a username and create the user itself.

### Request
- **Method:** `PUT`
- **Endpoint:** `/productvoucher/:voucher`
- **Full URL:** `https://api.minecraftservices.com/productvoucher/:voucher`
- **Headers:**
    - `Accept: application/json`
    - `Authorization: Bearer [JWT/auth token here]`

The only URL parameter here is the `voucher` parameter appended to the URL. This is the gift code or voucher we want to redeem.

### Response
- **Headers:**
    - `Content-Type: application/json`

**200: OK**

The voucher has been redeemed successfully. The following JSON response is returned on success:

```json
{
  "voucherInfo" : {
    "code" : "00000-00000-00000-00000-00000", // code redacted for safety
    "productVariant" : "minecraft", // could be "dungeons" for Minecraft Dungeons
    "status" : "ACTIVE"
  },
  "productRedeemable" : true // if you are allowed to redeem the code for an actual copy of the game
}
```

**401: Unauthorized**

You have not provided a valid JWT / auth token, or you have neglected to provide the `Authorization` header at all.

```json
{
  "path" : "/productvoucher/:voucher",
  "errorType" : "UnauthorizedOperationException",
  "error" : "UnauthorizedOperationException",
  "errorMessage" : "Unauthorized",
  "developerMessage" : "Unauthorized"
}
```

**404: Not Found**

You have not provided a valid voucher, or the voucher you provided has already been redeemed.

```json
// not a real code / invalid
{
  "path":"/productvoucher/:voucher",
  "errorType":"NOT_FOUND",
  "error":"NOT_FOUND"
}

// already used
{
  "path" : "/productvoucher/:voucher",
  "errorType" : "NOT_FOUND",
  "error" : "NOT_FOUND",
  "errorMessage" : "The server has not found anything matching the request URI",
  "developerMessage" : "The server has not found anything matching the request URI"
}
```

**500: Internal Server Error**

You are trying to redeem a voucher on an existing Mojang account. This doesn't work anymore. You must redeem vouchers on Microsoft accounts now.

```json
{
  "path" : "/productvoucher/:voucher",
  "errorType" : "No value present",
  "error" : "No value present"
}
```
