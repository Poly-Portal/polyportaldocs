# `POST` artworkFile/upload

## Description and Usage

This method uploads a file to the server. A 'file upload token' is required and can be obtained from [`artworkFile/create`](./create.md). Making the request consumes the token, regardless of if the request was successful or not. A user token is not required for this method. On success the sha-256 hash of the file will be returned which can be used to access the file.

## Key information

| Type | Value |
| - | - |
| Method | `POST` |
| Token | File upload token |
| HTTP content type | `multipart/form-data` |

## Required Arguments

None. Ensure you have a file upload token from [`artworkFile/create`](./create.md). The file is sent in the body as `multipart/form-data` content.

## Optional Arguments

None.

## Example Responses

### On Success

**Request:** `POST artworkFile/upload`

**Result:**
```json
{
  "ok":true,
  "file":{
    "sha256":"5e77061a9b955ac03d9a574a8a68d8a58005949fa4fdd3d9e38dbd263028ffe8",
  }
}
```

### On Error

**Request:** `POST artworkFile/upload`

**Result:**
```json
{
  "ok":false,
  "error":"badFile",
  "errorMessage":"The server rejected the file. The file may be corrupted or have an incorrect file extension."
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
| `invalidContentType` | The HTTP content type header was set incorrectly. It must be `multipart/form-data`. |
| `badFile` | The server rejected the file. The file may be corrupted or have an incorrect file extension. |
