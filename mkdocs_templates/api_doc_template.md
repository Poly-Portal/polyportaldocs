# `POST` 3DFile/upload

## Description and Usage

**Arguments must be sent in the message body as valid JSON.**

## Key information

| Type | Value |
| - | - |
| Method | `POST` |
| Token | User token |
| HTTP content type | `application/json` |

## Required Arguments


## Optional Arguments


## Example Responses

### On Success

**Request:** `POST `

**Request Body:**
```json

```

**Result:**
```json

```

### On Error

**Request:** `POST `

**Request Body:**
```json

```

**Result:**
```json

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


___
### `example`

Does the lorem ipsum

**Example:**
lorem ipsum

**Allowed values:**

* ``
* ``


___