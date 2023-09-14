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

Only artworks with a title matching the query string will be returned. The search is case-insensitive.

**Example:**
`artwork/list?title=Zebra`

**Allowed values:** Any string

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

### `createdBefore`

Only artworks with files created before the specified ISO 8601 date-time will be returned. This argument is timezone unaware, timezone information will be silently discarded.

**Example:**
`artwork/list?createdBefore=2023‐09‐07`

**Allowed values:** An ISO 8601 date-time.

___

### `createdAfter`

Only artworks with files created after the specified ISO 8601 date-time will be returned. This argument is timezone unaware, timezone information will be silently discarded.

**Example:**
`artwork/list?createdAfter=2023‐09‐07`

**Allowed values:** An ISO 8601 date-time.
___

### `tags`

Specifies the tags that should be matched. See the `tagMatchingStrategy` parameter to select if results must match either all of the tags or just one or more (defaults to any).

**Example (specifies "animals", "cars", and "music"):**
`artwork/list?tags=animals&tags=cars&tags=music`

**Allowed values:** Strings.
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
  "page":2,
  "lastPage":78,
  "artworks":[
    {
      "id":634,
      "title":"Aardvark",
      "downloads":4952,
      "views":73645,
      "current3DFiles":[
        {
          "sha256":"c7cf0b3ec6b78d30329ea4bf65f56121b0cf8f05f1b68a3d259b7cd00e113243",
          "extension":"fbx"
        },
        {
          "sha256":"4b1a5c87adc45123a290be68575072c880fa17e68c3b9e6cc74bbf16be5095c6",
          "extension":"fbx"
        }
      ],
      "tags":[
        "Animal",
        "Land animal"
      ]
    },
    {
      "id":126,
      "title":"Beaver",
      "downloads":52,
      "views":645,
      "current3DFiles":[
        {
          "sha256":"dde91fcdf38dc7e38739c99c1a873ed3979327d49d2f0e45e09a81417b4a3806",
          "extension":"fbx"
        }
      ],
      "tags":[
        "tags aren't always useful"
      ]
    },
    {
      "id":85765,
      "title":"Camel",
      "downloads":52221,
      "views":64345,
      "current3DFiles":[
        {
          "sha256":"e7070285bc228a6efc71835794f0f80b1181c2d8e30d48fe8ec733c7e2ee509e",
          "extension":"fbx"
        }
      ],
      "tags":[]
    }
  ]
}
```

* There is no guarantee that the number of artworks returned will be equal to the page size. 
  
* Successful queries will always return at least one artwork.
  
* The order of `"current3DFiles"` is guaranteed to be the same across requests.

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
| `invalidParameterValue` | The value of one or more parameters was formatted incorrectly or had an illegal value. |
| `unknownParameterValue` | One or more of the URL parameters was unknown. |
| `noArtworksFound` | No artworks were found that matched the query. |
| `pageLimitExceeded` | The page specified is greater than the total amount of pages at the given page size. |

