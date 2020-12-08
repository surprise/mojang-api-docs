# Authenticating a Microsoft account
This article aims to partially document how to log in to a Microsoft account to authenticate with Minecraft.

**WARNING:** This is not a finished article!

First, you must obtain your XBL3.0 token. This [StackOverflow answer](https://stackoverflow.com/a/52111578) shows a way to get the XBL3.0 token in Python. If you take a peek at the source of the referenced library, you can make your own token grabber in your own language. This will be documented at some point later on in time.

Next, send a `POST` request to `https://api.minecraftservices.com/authentication/login_with_xbox`. The POST body should be similar to:
```json
{
   "identityToken" : "XBL3.0 x=uhs;xsts",
   "ensureLegacyEnabled" : true
}
```

You must send this request with the `Content-Type: application/json` header.

You will get a response similar to this:

```json
{
  "username" : "830491e6-50e9-e9ed-6e8a-7041f4fef585", // Xbox account username
  "roles" : [ ], // i suppose this will have something in it if the account has a copy of Minecraft
  "access_token" : "eyJhbGciOiJIUzI1NiJ9.eyJ4dWlkIjoiMjUzMzI3NDgwNTgyOTU2OCIsInN1YiI6IjgzMDQ5MWU2LTUwZTktZTllZC02ZThhLTcwNDFmNGZlZjU4NSIsIm5iZiI6MTYwNjg0NTE0Niwicm9sZXMiOltdLCJpc3MiOiJhdXRoZW50aWNhdGlvbiIsImV4cCI6MTYwNjkzMTU0NiwiaWF0IjoxNjA2ODQ1MTQ2LCJ5dWlkIjoiNTRmYzUwYzFiMWJjMTlkZDEwOWZiZWZmOWQxMWJmNDEifQ.-7H1jT3i54gmbqQcUBdHArOn-Jr8eZVAyPDiOr5q_XY", // access token
  "token_type" : "Bearer", // don't think there are other types
  "expires_in" : 86400 // number of seconds until token expires. MSA tokens last 24 hours. yes, really, 24 hours!
}
```

The `access_token` is what you will now use to authenticate yourself to other API endpoints.

See the "A peek into Bearer tokens" article for more information about what's inside the `access_token`.


