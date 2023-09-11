# `POST` artwork/remove

## Description and Usage

Remove an artwork, preventing access to it. The artwork will still be preserved on disk. Optionally removes associated 3D files (default behavior is to remove). On success a list of orphaned 3D files will be returned (if no files were orphaned, such as if they were all removed, an empty list is returned).

**Arguments must be sent in the message body as valid JSON.**

## Key information

| Type | Value |
| - | - |
| Method | `POST` |
| Token | User token |
| HTTP content type | `application/json` |

## Required Arguments

___
### `file`

The artwork to be removed. The user must have permissions over the artwork.

**Example:**
```json
{
  "artworkID":9785
}
```

**Allowed values:** An artwork ID.

___

## Optional Arguments

___
### `remove3DFiles`

If 3D files associated with the artwork should also be removed. The function is equivalent to [`3DFile/remove`](../3DFile/remove.md) Default = `true`.

**Example:**
```json
{
  "remove3DFiles":false
}
```

**Allowed values:** `true` or `false`.

___


## Example Responses

### On Success

**Request:** `POST artwork/remove`

**Request Body:**
```json
{
  "artworkID":9785,
  "remove3DFiles":false
}
```

**Result:**
```json
{
  "ok":true,
  "orphanedFiles":[
    {
      "sha256":"5e77061a9b955ac03d9a574a8a68d8a58005949fa4fdd3d9e38dbd263028ffe8",
      "extension":"obj"
    }
  ]
}
```

### On Error

**Request:** `POST artwork/remove`

**Request Body:**
```json
{
  "artworkID":"should be an integer",
}
```

**Result:**
```json
{
  "ok":false,
  "error":"invalidArgument",
  "errorMessage":"Parameter 'artworkID' had an invalid value"
}
```
git 
## Errors

The following list may not be exhaustive. Callers should always check the `ok` parameter of the JSON.

| Error | Description |
| - | - |
| `accessDenied` | Access to the specified resource is denied. |
| `tokenExpired` | The token has expired. |
| `tokenMissing` | No token was provided. |
| `unavailable` | The service is temporarily unavailable. |
| `internalError` | The request could not be completed due to an internal error. It is possible some of the request was carried out. |
| `invalidContentType` | The HTTP content type header was set incorrectly. It must be `application/JSON`. |
| `invalidArgument` | One or more of the arguments had an invalid or illegal value. |
| `unknownArgument` | One or more arguments were unknown. |
| `missingRequiredArgument` | One or more of the required arguments was missing. |
| `badJSON` | The JSON provided could not be parsed. |
| `noSuchArtwork` | There was no artwork matching the reference or the user does not have permission to access that artwork. |


