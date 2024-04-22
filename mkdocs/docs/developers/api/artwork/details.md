# `GET` artwork/list

## Description and Usage

Returns all known details of a specified artwork, with signed URLS to files.

**Arguments must be passed as URL parameters.**

## Key information

| Type | Value |
| - | - |
| Method | `GET` |
| Token | User token |
| HTTP content type | N/A |

## Required Arguments

### `artworkId`

The id of the artwork you want details for.

**Example**
`artwork/details?artworkId=46345`

**Allowed Values**
A valid artwork id.

___

## Example Responses

### On Success

**Query:** `artwork/artwork?pageSize=3&page=2&sortOrder=lexicographical`

**Result:**
```json
{
  "ok":true,
  "artwork":{
    "id":"64",
    "title":"teapot",
    "description":"",
    "downloads":40,
    "views":561,
    "createdAt":"2024-04-21T22:59:42.291Z",
    "files":{
      "models":[
        {
          "fileId":"122",
          "fileName":"My_Cool_File",
          "fileExtension":"fbx",
          "signedURL":"https://poly-portal-files.s3.ap-southeast-2.amazonaws.com/122?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIA2OYZ4MVHCXYHVNHH%2F20240422%2Fap-southeast-2%2Fs3%2Faws4_request&X-Amz-Date=20240422T094847Z&X-Amz-Expires=3600&X-Amz-Signature=f7cb6b9216bdf2f994946905ab75b2a90607a17541adbd7d5a20cc708dcd8e1f&X-Amz-SignedHeaders=host&x-id=GetObject",
          "signedURLExpiryTimeSeconds":"3600"
        }
      ],
      "textures":[
        
      ],
      "materials":[
        
      ],
      "thumbnails":[
        
      ],
      "other":[
        
      ]
    },
    "tags":[
      
    ]
  }
}
```

### On Error

**Query:** `artwork/list?artworkId=Im_Not_An_ID`

**Result:**
```json
{
  "ok":false,
  "error":"invalidParameterValue",
  "errorMessage":"Parameter 'artworkId' had an invalid value."
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
| `noArtworksFound` | No artworks were found that matched the query. |
| `invalidArgument` | One or more of the arguments had an invalid or illegal value. |
| `unknownArgument` | One or more arguments were unknown. |
| `missingRequiredArgument` | One or more of the required arguments was missing. |

