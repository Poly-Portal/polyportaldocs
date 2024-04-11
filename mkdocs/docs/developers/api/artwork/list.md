# `GET` artwork/list

## Description and Usage

Returns a paginated list of artworks in a specified sort order. The list can be additionally filtered using optional search parameters. 

**Arguments must be passed as URL parameters.**

## Key information

| Type | Value |
| - | - |
| Method | `GET` |
| Token | User token |
| HTTP content type | N/A |

## Required Arguments

None.


## Optional Arguments

___

### `sortOrder`

Specifies the order that artworks should be returned in, such as in order of creation. Default = `downloads`.

**Example:**
`artwork/list?sortOrder=downloads`

**Allowed values:**

* `downloads`: sort in order of downloads.
* `views`: sort in order of views.
* `lexicographical`: sort in lexicographical (alphabetical) order.
* `uploadDate`: sort by most recently uploaded.

___

### `sortDescending`

Specifies if the sort order should be descending (`true`) or ascending (`false`). Default = `true`.

**Example:**
`artwork/list?sortDescending=false`

**Allowed values:** `true` or `false`
___
### `pageSize`

How many results should be returned on a page. Default is 25.

**Example:**
`artwork/list?pageSize=50`


**Allowed values:** Positive integers 1 <= x <= 100.

___

### `page`

Which page to return, relating to pagination. Pages start at 1. Default is 1.

**Example:**
`artwork/list?page=2`

**Allowed values:** Positive integers 1 or greater.

___

### `fileExtension`

Only artworks with the specified file extension will be returned. **The file extension should not have a dot (.) at the front.**

**Example:**
`artwork/list?fileExtension=fbx`

**Allowed values:** A file extension without a preceding dot.

___

### `title`

Only artworks with a title exactly matching the query string will be returned. 

**Example:**
`artwork/list?title=Zebra`

**Allowed values:** Any non empty string

___

### `uploadedBefore`

Only artworks uploaded before the specified timestamp will be returned. 

**Example:**
`artwork/list?uploadedBefore=1694085155`

**Allowed values:** UNIX timestamp in integer seconds.

___

### `uploadedAfter`

Only artworks uploaded after the specified timestamp will be returned. 

**Example:**
`artwork/list?uploadedAfter=1694085155`

**Allowed values:** UNIX timestamp in integer seconds.

___

### `tags`

Specifies the tags that should be matched. See the `tagMatchingStrategy` parameter to select if results must match either all of the tags or just one or more (defaults to any).

**Example (specifies "animals", "cars", and "music"):**
`artwork/list?tags=animals&tags=cars&tags=music`

**Allowed values:** One or more none empty strings.
___

### `tagMatchingStrategy`

Specifies the matching criteria for tags. If this parameter is used you must also specify the `tags` parameter.

* `all`: Will only return artworks that have all of the tags specified
* `any`: Will only return artworks that have at least one of the tags specified.

Default = `any`.

**Example:** `artwork/list?tagMatchingStrategy=all`

**Allowed values:** `any` or `all`.

___

## Example Responses

### On Success

**Query:** `artwork/list?pageSize=3&page=2&sortOrder=lexicographical`

**Result:**
```json
{
  "ok":true,
  "pageSize":3,
  "page":1,
  "lastPage":5,
  "artworks":[
    {
      "id":"21",
      "title":"Nation still.",
      "downloads":4037,
      "views":750,
      "createdAt":1369539861,
      "files":{
        "models":[
          
        ],
        "textures":[
          {
            "fileId":"52",
            "fileName":"71",
            "fileExtension":"glb",
            "signedURL":null,
            "signedURLExpiryTimeSeconds":null
          }
        ],
        "materials":[
          
        ],
        "thumbnails":[
          {
            "fileId":"95",
            "fileName":"56",
            "fileExtension":"fbx",
            "signedURL":null,
            "signedURLExpiryTimeSeconds":null
          }
        ],
        "other":[
          
        ]
      },
      "tags":[
        "Member.",
        "Same."
      ]
    },
    {
      "id":"20",
      "title":"Fish magazine.",
      "downloads":2837,
      "views":4072,
      "createdAt":1075818863,
      "files":{
        "models":[
          {
            "fileId":"34",
            "fileName":"88",
            "fileExtension":"glb",
            "signedURL":null,
            "signedURLExpiryTimeSeconds":null
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
        "Alone.",
        "More."
      ]
    },
    {
      "id":"26",
      "title":"Alone.",
      "downloads":61,
      "views":4268,
      "createdAt":72198176,
      "files":{
        "models":[
          
        ],
        "textures":[
          {
            "fileId":"69",
            "fileName":"25",
            "fileExtension":"fbx",
            "signedURL":null,
            "signedURLExpiryTimeSeconds":null
          }
        ],
        "materials":[
          
        ],
        "thumbnails":[
          {
            "fileId":"46",
            "fileName":"84",
            "fileExtension":"glb",
            "signedURL":null,
            "signedURLExpiryTimeSeconds":null
          }
        ],
        "other":[
          
        ]
      },
      "tags":[
        
      ]
    }
  ]
}
```

* There is no guarantee that the number of artworks returned will be equal to the page size. 
  
* Successful queries will always return at least one artwork.
  
* The order of files is guaranteed to be the same across requests.

### On Error

**Query:** `artwork/list?sortOrder=WRONG`

**Result:**
```json
{
  "ok":false,
  "error":"invalidParameterValue",
  "errorMessage":"Parameter 'sortOrder' had an invalid value."
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
| `pageLimitExceeded` | The page specified is greater than the total amount of pages at the given page size. |
| `invalidArgument` | One or more of the arguments had an invalid or illegal value. |
| `unknownArgument` | One or more arguments were unknown. |
| `missingRequiredArgument` | One or more of the required arguments was missing. |

