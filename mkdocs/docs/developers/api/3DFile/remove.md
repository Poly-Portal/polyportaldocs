# `POST` 3DFile/remove

## Description and Usage

Remove a 3D file, preventing access to it. The file itself will be preserved on disk. The file must not be associated with an artwork.

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

The file reference (sha-256) of the file to be deleted. The file may not be in use by an artwork.

**Example:**
```json
{
  "file":"6b34652fb313f2ebbbd086a222a1b7ad60d0add0aea753e451b94230eb4e5a1e"
}
```

**Allowed values:** A string matching a file reference.

___

## Optional Arguments


## Example Responses

### On Success

**Request:** `POST 3DFile/remove`

**Request Body:**
```json
{
  "file":"6b34652fb313f2ebbbd086a222a1b7ad60d0add0aea753e451b94230eb4e5a1e"
}
```

**Result:**
```json
{
  "ok":true
}
```

### On Error

**Request:** `POST 3DFile/remove`

**Request Body:**
```json
{
  "file":"not_a_valid_file_reference"
}
```

**Result:**
```json
{
  "ok":false,
  "error":"noSuchFile",
  "errorMessage":"There was no file matching the reference or the user does not have permission to access that file."
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
| `noSuchFile` | There was no file matching the reference or the user does not have permission to access that file. |
| `fileInUse` | The file is referenced by an artwork. Remove the artwork first. |


