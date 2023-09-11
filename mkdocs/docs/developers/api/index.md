# API Documentation

Poly Portal uses a REST style API to communicate between server and client. Outbound content (from the server to the client) is retrieved via `GET` request and inbound content (from the client to the server) is delivered via a `POST` request`*`.

`*` There is additional complexity around file uploads. This is explained in the relevant sections.

## Overview

### `GET` Requests

`GET` requests accept url parameters and returns JSON. Example URL parameter: `www.abc.com/page?key1=value1&key2=value2`.

A valid token must be provided in the HTTP `Authorization` header.

### POST Requests (Excluding File Upload)

`POST` accepts JSON bodies as an input and will return JSON.

The HTTP `Content-type` header **must** be set to `application/json`.

A valid token must be provided in the HTTP `Authorization` header.

### POST Request (File Upload Only)

`POST` requests for file uploads **must** have the HTTP `Content-type` header set to `multipart/form-data`

A special file upload token must be provided in the HTTP `Authorization` header. This token is unique to the file being uploaded.


## Important Terms and Nomenclature.

* **3D Files**: A 3D file is an individual file containing 3d assets. Such files include .FBX and .OBJ files.
  
* **Artworks**: An artwork is a *collection* of one or more *3D files.* One artwork may contain many *3D files.* Artworks may also have many versions.

## HTTP Response Codes and Error Handling
Generally, this API does not make use of HTTP response codes. In normal operation, the API will return a HTTP 200 code with a JSON response in the body, regardless of if the request was successful or not.

Callers may check if a request was successful using the `ok` field in the attached JSON. On success the `ok` field will be set to `true`. On failure the `ok` field will be set to `false` and an error code and message will be included.

**An example of a successful response:**
```json
{
  "ok":true
  ... other JSON data ...
}
```

**An example of a failed response:**
```json
{
  "ok":false,
  "error":"accessDenied",
  "errorMessage":"Access to the specified resource is denied."
}
```

## Tokens and The Authorization Header
There are two types of tokens. To maintain security the tokens must be kept secret. Tokens are included plaintext in the authorization header using the basic authorization scheme.  

* **User tokens.** User tokens are issued to users when they log in and are used for most API features. The token uniquely identifies the user.
* **File upload tokens**. File upload tokens are issued when uploading a file. When a request is made using a file upload token the token is consumed and another must be generated. See [`3DFile/create`](3DFile/create.md) and [`3DFile/upload`](3DFile/upload.md) for more information.

## Quick reference
TODO

## Endpoints

| Type | Endpoint | Description |
| ---- | -------- | ----------- |
| `GET` | [`artwork/list`](artwork/list.md) | Get a list of artworks matching search parameters in a specified order. |
| `POST` | [`artwork/create`](artwork/create.md) | Create a new artwork. |
| `POST` | [`artwork/update`](artwork/update.md) | Create a new version of the artwork. |
| `POST` | [`artwork/remove`](artwork/remove.md) | Remove an artwork. |
| `POST` | [`3DFile/create`](3DFile/create.md) | Inform the server of your intention to upload a 3D file. |
| `POST` | [`3DFile/upload`](3DFile/upload.md) | Upload a 3D file using the details from `3DFile/create`. |
| `POST` | [`3DFile/remove`](3DFile/remove.md) | Delete a 3D file. |
| `POST` | [`user/login`](user/login.md) | Login an existing user. |
| `POST` | [`user/register`](user/register.md) | Register a new user. |
| `POST` | [`user/logout`](user/logout.md) | Revoke all tokens issued to a user. |

