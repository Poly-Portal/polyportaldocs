# `POST` 3DFile/create

## Description and Usage

This method is used with its companion method [`3DFile/upload`](./upload.md) to upload files to the server. This method informs the server of your intention to upload a file and provides a one time use 'file upload token' that is required by `3DFile/upload`. The token is valid until the time indicated in the response or until it has been used.

**Arguments must be sent in the message body as valid JSON.**

## Key information

| Type | Value |
| - | - |
| Method | `POST` |
| Token | User token |
| HTTP content type | `application/json` |

## Required Arguments

___
### `fileExtension`

The file extension of the file that will be uploaded. **The file extension should not have a dot (.) at the front.**

**Example:**
```json
{
  "fileExtension":"fbx"
}
```

**Allowed values:** The file extension (without a preceding dot) of a file to uploaded. Specifying the wrong extension is likely to cause `3DFile/upload` to fail.

Allowed file types (case insensitive):

* `fbx`
  
* `obj`
  
* `stl`
  
* `stp`
  
* `glb`
  
* `gltf`
___

## Optional Arguments

None.

## Example Responses

### On Success

**Request:** `POST 3DFile/create`

**Request Body:**
```json
{
  "fileExtension":"fbx"
}
```

**Result:**
```json
{
  "ok":true,
  "fileUploadToken":"AYjcyMzY3ZDhiNmJkNTY",
  "secondsToExpiry":3600
}
```

### On Error

**Request:** `POST 3DFile/create`

**Request Body:**
```json
{
  "unknown":"abc123"
}
```

**Result:**
```json
{
  "ok":false,
  "error":"unknownArgument",
  "errorMessage":"Unknown argument was passed. Allowed arguments are: `fileExtension`."
}
```


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

