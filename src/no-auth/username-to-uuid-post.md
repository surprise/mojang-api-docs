# Username to UUID (POST)
This endpoint allows users to send up to 10 usernames in an array and return all valid UUIDs.

### Request
- **Method:** `POST`
- **Endpoint:** `/profiles/minecraft`
- **Full URL:** `https://api.mojang.com/profiles/minecraft`
- **Headers:**
    - `Content-Type: application/json`

The JSON body of the request must look similar to this (of course, supplying your own usernames):

```json
[
  "lukethehacker23",
  "Hacker",
  "Unpredictable",
  "Await",
  "tanpug",
  "Dusks"
]
```

### Response
**200: OK**

There were no errors with the request. You may still get a `200 OK` response if none of the names you provided correspond to a valid Minecraft profile - you will just get an empty array. Sample responses are below:

```json
// no valid Minecraft profiles were found for any of the requested usernames
[]

// valid Minecraft profiles were found - they are sorted when returned
[
  {
    "id" : "cdb5aee80f904fdda63ba16d38cd6b3b", // UUID of account
    "name" : "lukethehacker23" // account username
  },
  {
    "id" : "e426cee9bd5044f6b4d9628b981d36a0", // UUID of account
    "name" : "Await" // account username
  },
  {
    "id" : "8af296533b6844d085932742dca689c9", // UUID of account
    "name" : "Dusks" // account username
  },
  {
    "id" : "dd5e3b0b6d2440d2a740ebdbddb6e76b", // UUID of account
    "name" : "Hacker" // account username
  },
  {
    "id" : "f0d9de88bbb54c9eae429cd8fbd693ab", // UUID of account
    "name" : "tanpug" // account username
  },
  {
    "id" : "c3d8e16622234b6bb6bcccf7907fb35a", // UUID of account
    "name" : "Unpredictable" // account username
  }
]
```

**400: Bad Request**

You could have gotten this error either because you've supplied an invalid username as one of the names in the array you sent as the POST body, because you supplied invalid JSON as the POST body, or because you supplied more than 10 names in the POST body.

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

// invalid JSON
{
  "error" : "JsonMappingException",
  "errorMessage" : "Unexpected character ('\"' (code 34)): was expecting comma to separate Array entries\n at [Source: (org.eclipse.jetty.server.HttpInputOverHTTP); line: 1, column: 118] (through reference chain: java.lang.Object[][7])"
}

// more than 10 names
{
  "error" : "IllegalArgumentException",
  "errorMessage" : "Not more that 10 profile name per call is allowed."
}
```

**405: Method Not Allowed**

You did not make the request a POST request.

```json
{
  "error" : "Method Not Allowed",
  "errorMessage" : "The method specified in the request is not allowed for the resource identified by the request URI"
}
```

**415: Unsupported Media Type**

When encountering this error, you have most likely neglected to add the `Content-Type: application/json` header to your request.

```json
{
  "error" : "Unsupported Media Type",
  "errorMessage" : "The server is refusing to service the request because the entity of the request is in a format not supported by the requested resource for the requested method"
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
