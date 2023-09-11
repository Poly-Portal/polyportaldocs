# `POST` artwork/create

## Description and Usage

Creates an artwork, linking 3D files to it and giving them a joint title and description. Will return the ID of the new artwork upon success.

**Arguments must be sent in the message body as valid JSON.**

## Key information

| Type | Value |
| - | - |
| Method | `POST` |
| Token | User token |
| HTTP content type | `application/json` |

## Required Arguments

___
### `title`

Specifies the title of the artwork.

**Example:**
```json
{
  "title":"Fly Me to the Moon"
}
```

**Allowed values:** any string.

___

### `3DFiles`

Specifies the files included in this artwork. The files must not already be included in an artwork. The user making the request must be the owner of the files.

**Example:**
```json
{
  "3DFiles":[
    "2ba58048d97a6adefa8089b60322933489d07ba0b58f6528a07980142a7ccf5c",
    "fcd91acd1fe9e861082e5a6346ad430feb6c14452308cf79e515a1906fa3b22d"
  ]
}
```

**Allowed values:** A list of valid file references that are not used in other artworks and are owned by the user.

___

## Optional Arguments


___

### `description`

Specifies the description of the artwork. The default description is `""` (empty string).

**Example:**
```json
{
    "description":"I worked really hard on this !11!!1!"
}
```

**Allowed values:** any string.

___


## Example Responses

### On Success

**Request:** `POST artwork/create`

**Request Body:**
```json
{
  "title":"WALL-E",
  "description":"EVAAAAAA!",
  "3DFiles":[
    "3366fd48dc0860585d8c11e7262168b54649d3bb1d3f62c2b6e79597a21ca9d2"
  ]
}
```

**Result:**
```json
{
    "ok":true,
    "artworkID":5475
}
```

### On Error

**Request:** `POST artwork/create`

**Request Body:**
```json
{
  "title":"The 3d files field contains duplicates.",
  "description":"It will result in an error.",
  "3DFiles":[
    "a5cfb7e8c5cc4a07081885f06de2606c0bd3de8db8ebf49b32681679195e82bc",
    "a5cfb7e8c5cc4a07081885f06de2606c0bd3de8db8ebf49b32681679195e82bc"
  ]
}
```

**Result:**
```json
{
    "ok":false,
    "error":"duplicateFile",
    "errorMessage":"A 3D file was included in the artwork more than once."
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
| `duplicateFile` | A 3D file was included in the artwork more than once. |
