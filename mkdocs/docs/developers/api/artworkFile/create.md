# `POST` artworkFile/create

## Description and Usage

This endpoint is used in preparation for uploading a file. The response will contain a location and fields to send a POST request to S3 in order to complete the upload. The POST request is signed and will only be valid for a set period. 

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

**Allowed values:** The file extension (without a preceding dot) of a file to uploaded. Specifying the wrong extension is likely to cause `3DFile/upload` to fail. Any string is accepted.


### `fileName`

The name of the file that will be uploaded. This is not required to include the dot (.) used for the file extension.

**Example:**
```json
{
  "fileName":"My_c00l_m0del"
}
```

**Allowed values:** Any string.

___

## Optional Arguments

None.

## Example Responses

### On Success

**Request:** `POST 3DFile/create`

**Request Body:**
```json
{
  "fileName":"C3PO",
  "fileExtension":"fbx"
}
```

**Result:**
```json
{
  "ok":true,
  "fileId":"114",
  "signedPOST":{
    "url":"https://poly-portal-files.s3.ap-southeast-2.amazonaws.com/",
    "fields":{
      "acl":"private",
      "bucket":"poly-portal-files",
      "X-Amz-Algorithm":"AWS4-HMAC-SHA256",
      "X-Amz-Credential":"AKIA2OYZ4MVHCXYHVNHH/20240411/ap-southeast-2/s3/aws4_request",
      "X-Amz-Date":"20240411T080107Z",
      "key":"113",
      "Policy":"eyJleHBpcmF0aW9uIjoiMjAyNC0wNC0xMVQwOTowMTowN1oiLCJjb25kaXRpb25zIjpbWyJlcSIsIiRhY2wiLCJwcml2YXRlIl0sWyJlcSIsIiRidWNrZXQiLCJwb2x5LXBvcnRhbC1maWxlcyJdLFsiZXEiLCIka2V5IiwiMTEzIl0seyJhY2wiOiJwcml2YXRlIn0seyJidWNrZXQiOiJwb2x5LXBvcnRhbC1maWxlcyJ9LHsiWC1BbXotQWxnb3JpdGhtIjoiQVdTNC1ITUFDLVNIQTI1NiJ9LHsiWC1BbXotQ3JlZGVudGlhbCI6IkFLSUEyT1laNE1WSENYWUhWTkhILzIwMjQwNDExL2FwLXNvdXRoZWFzdC0yL3MzL2F3czRfcmVxdWVzdCJ9LHsiWC1BbXotRGF0ZSI6IjIwMjQwNDExVDA4MDEwN1oifSx7ImtleSI6IjExMyJ9XX0=",
      "X-Amz-Signature":"96bf8fb91251f30970c2a49ad54d765d13cba776d714f5427d38ff07902266d5"
    }
  },
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
  "errorMessage":"Unknown argument was passed. Allowed arguments are: 'fileExtension', 'fileName'."
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

