# `POST` artwork/update

## Description and Usage

May be used to change the title of an artwork, modify the description, and/or update what files are associated with the artwork.

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

### `files`

Specifies the files included in this artwork. The files may already be included in the artwork or they may be files not included in any artwork. The user must have permission to use the files. The updated list of files must not be identical to the current list of files - if the files are not being updated do not use this argument.

The behavior is the same as the 'files' argument for the [artwork/create](./create.md#files) endpoint.

**Example:**
```json
{
  "files":{
    "models":[
      "c7cf0b3ec6b78d30329ea4bf65f56121b0cf8f05f1b68a3d259b7cd00e113243"
    ],
    "textures":[
      "2f33b1f6e25d5d0ded190b8a70ae253c6112c834b3b45640236452b57811b4e7",
      "eca0f1c7112438a1bd2f6ccdb433e8138662d6b406425dd48228ef25c14c0a12"
    ],
    "materials":[
      "eca0f1c7112438a1bd2f6ccdb433e8138662d6b406425dd48228ef25c14c0a12"
    ],
    "thumbnails":[
      "1f33b7baff0ec4b46a508deb9db1c6f5844de78205935b54d7bb7e45ec1ac30c"
    ],
    "other":[
      "7112026d192c74cf7fb325dd5f0ad1d603d0689faebee84fd6a6babf0a3b6f7f"
    ]
  }
}
```

**Allowed values:** A list of valid file references that are not used in other artworks and are the user has permission to use. Additional restrictions may be placed on what files may be used for a specific purpose. For example, a JPEG is not a model.

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

### `tags`

Specifies the tags for the artwork. If this parameter is not specified than the tags will not be changed. Using this argument will remove any tags that do not appear in the list. 

**Example:**
```json
{
  "tags":[
    "wildlife",
    "animals",
    "nature"
  ]
}
```

**Allowed values:** A list of strings.

___


## Example Responses

### On Success

**Request:** `POST artwork/create`

**Request Body:**
```json
{
  "artworkID":12477,
  "title":"This is the updated title",
  "description":"This is the new description",
  "tags":[
    "updated tags",
    "old ones not in this list will be removed"
  ]
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
  "files":[]
}
```

**Result:**
```json
{
  "ok":false,
  "error":"noFilesSpecified",
  "errorMessage":"An artwork must specify at least one model file."
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
| `duplicateFile` | A file was included in the artwork more than once. |
| `noFilesSpecified` | An artwork must specify at least one file. |
| `noFilesChanged` | The updated list of files is the same as the current list of files.  |
| `noSuchArtwork` | There was no artwork matching the reference or the user does not have permission to access that artwork. |
| `unsuitableFile` | A file was specified for an unsuitable purpose (e.g. an image used as a model). |


