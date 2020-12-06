# View user information
This endpoint allows an authenticated user to view their user information (birthday, `userId` value, email, if it has security questions, etc).

### Request
- **Method:** `GET`
- **Endpoint:** `/user`
- **Full URL:** `https://api.mojang.com/user`
- **Headers:**
    - `Authorization: Bearer [JWT/auth token here]`

You must have answered your security questions described in the Security Question-Answer Flow article in order to use this endpoint.

### Response
**200: OK**

No errors occurred when fetching user information. Sample response below (for both migrated / Mojang accounts and unmigrated / legacy accounts):

```json
// migrated account (Mojang account)
{
   "id":"026cb82ad0c006a2d7e4fe9df19620ad", // userId value (internal Mojang account identifier, NOT uuid)
   "email":"coolemail@domain.tld", // email of account
   "username":"coolemail@domain.tld", // the username is the email for migrated accounts
   "dateOfBirth":849624812000, // account's date of birth in Unix epoch time
   "secured":true, // does the account have security questions?
   "emailVerified":true, // is the email verified?
   "legacyUser":false, // is the account legacy?
   "verifiedByParent":false, // does the account have parental consent?
   "hashed":false // is the email hashed?
}

// unmigrated / legacy account
{
  "id": "1253680", // userId value (internal Mojang account identifier, NOT uuid)
  "email": "N/A", // previously was the email hashed in md5 format
  "username": "coolusername2", // account username (coolusername2 is not the actual username of the test account I used)
  "secured": false, // does the account have security questions? (legacy accounts can't)
  "emailVerified": true, // is the email verified?
  "legacyUser": true, // is the account legacy?
  "verifiedByParent": false, // does the account have parental consent?
  "hashed": true // is the email hashed? (it is for legacy accounts, but the API doesn't show them anymore)
}
```

**401: Unauthorized**

This error occurs when you either haven't answered your security questions, or when you've passed an invalid or expired Bearer token in the `Authorization` header.

```json
{
  "error" : "UnauthorizedOperationException",
  "errorMessage" : "User not authenticated"
}
```
