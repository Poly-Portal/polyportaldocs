# `POST` artwork/update

## Description and Usage

May be used to change the title of an artwork, modify the description, and/or update what 3D files are associated with the artwork.

**At least one of the optional arguments must be specified.**

**Arguments must be sent in the message body as valid JSON.**

## Key information

| Type | Value |
| - | - |
| Method | `POST` |
| Token | User token |
| HTTP content type | `application/json` |

## Required Arguments

___

### `artworkID`

The ID of the artwork to be updated. The user must have permissions over the artwork specified.

**Example:**
```json
{
  "artworkID":4672
}
```

**Allowed values:** An artwork ID.

___


## Optional Arguments (include at least one)


___
### `title`

Specifies the title of the artwork.

**Example:**
```json
{
  "title":"Hyper-Realistic Schweppes Lemonade Can"
}
```

**Allowed values:** any string.

___

### `3DFiles`

Specifies the files included in this artwork. The files may already be included in the artwork or they may be files not included in any artwork. The files must not be included in any *other* artwork and must be owned by the user. The updated list of files must not be identical to the current list of files - if the files are not being updated do not use this argument.

**Example:**
```json
{
  "3DFiles":[
    "2ba58048d97a6adefa8089b60322933489d07ba0b58f6528a07980142a7ccf5c",
    "fcd91acd1fe9e861082e5a6346ad430feb6c14452308cf79e515a1906fa3b22d"
  ]
}
```

**Allowed values:** A list of valid file references. See above.

___

### `description`

Specifies the description of the artwork.

**Example:**
```json
{
    "description":"Writing descriptions is hard."
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
  "artworkID":12477,
  "title":"This is the updated title",
  "description":"This is the new description"
}

```

**Result:**
```json
{
  "ok":true
}
```

### On Error

**Request:** `POST artwork/create`

**Request Body:**
```json
{
  "artworkID":12477,
  "3DFiles":[]
}
```

**Result:**
```json
{
  "ok":false,
  "error":"noFilesSpecified",
  "errorMessage":"An artwork must specify at least one 3D file."
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
| `noFilesSpecified` | An artwork must specify at least one 3D file. |
| `noFilesChanged` | The updated list of 3D files is the same as the current list of 3D files.  |
| `noSuchArtwork` | There was no artwork matching the reference or the user does not have permission to access that artwork. |

