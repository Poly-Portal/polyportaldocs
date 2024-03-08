# `POST` artwork/create

## Description and Usage

Creates an artwork, linking files to it and giving them a joint title and description. Will return the ID of the new artwork upon success.

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

### `files`

Specifies the artwork files included in this artwork. The user making the request must have permission to use the files.

The purpose of the file must also be specified, it may be a model, texture, material, thumbnail or 'other' file. At least one model must be specified. Other fields (`textures`, `materials`, `thumbnails`, and `other`) may be omitted.

**Example 1:**
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

**Example 2:**
```json
{
  "files":{
    "models":[
      "c7cf0b3ec6b78d30329ea4bf65f56121b0cf8f05f1b68a3d259b7cd00e113243"
    ]
  }
}
```

**Allowed values:** A list of valid file references that are not used in other artworks and are the user has permission to use. Additional restrictions may be placed on what files may be used for a specific purpose. For example, a JPEG is not a model.

___

## Optional Arguments

None.
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

### `tags`

Specifies the tags for the artwork. The default is to have no tags.

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
  "title":"WALL-E",
  "description":"EVAAAAAA!",
  "files":{
    "models":[
      "3366fd48dc0860585d8c11e7262168b54649d3bb1d3f62c2b6e79597a21ca9d2"
    ]
  },
  "tags":[
    "robot",
    "movies"
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
  "title":"The textures field contains duplicates.",
  "description":"It will result in an error.",
  "files":{
    "models":[
      "a5cfb7e8c5cc4a07081885f06de2606c0bd3de8db8ebf49b32681679195e82bc"
    ],
    "textures":[
      "fd168422daf7f4017039ac8c60e5cab64bc3707134d554689f2eec2a7dfa1795",
      "fd168422daf7f4017039ac8c60e5cab64bc3707134d554689f2eec2a7dfa1795"
    ]
  }
}
```

**Result:**
```json
{
  "ok":false,
  "error":"duplicateFile",
  "errorMessage":"A file was included in the artwork more than once."
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
| `unsuitableFile` | A file was specified for an unsuitable purpose (e.g. an image used as a model). |
