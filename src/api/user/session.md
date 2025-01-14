# Session Management

These endpoints pertains to the various actions that can be performed on sessions of the authenticated user.

## GET /user/session

Get the current session used to authenticate.

:::details Example Request

<code-group>

<code-block title="cURL">

```sh
curl -X GET \
  -H "Authorization: token" \
  https://alekeagle.me/api/user/session
```

</code-block>

<code-block title="JS Fetch">

```js
fetch('https://alekeagle.me/api/user/session', {
  method: 'GET',
  credentials: 'include',
  headers: {
    Authorization: 'token'
  }
});
```

</code-block>

</code-group>

:::

:::details Responses

- 200 OK

  - [Session](/reference/structures/errors.md#session)

- 401 Unauthorized

  - [InvalidSession](/reference/structures/errors.md#invalidsession)

- 403 Forbidden

  - [Banned](/reference/structures/errors.md#banned)

- 429 Too Many Requests

  - [RateLimited](/reference/structures/errors.md#ratelimited)

- 500 Internal Server Error

  - [Internal](/reference/structures/errors.md#internal)

:::

## GET /user/session/:id

Get a specific session owned by the authenticated user.

:::details Parameters

- Path

  - `id`

    - The ID of the session you want more info about.

:::

:::details Example Request

<code-group>

<code-block title="cURL">

```sh
curl -X GET \
  -H "Authorization: token" \
  https://alekeagle.me/api/user/session/1234567890
```

</code-block>

<code-block title="JS Fetch">

```js
fetch('https://alekeagle.me/api/user/session/1234567890', {
  method: 'GET',
  credentials: 'include',
  headers: {
    Authorization: 'token'
  }
});
```

</code-block>

</code-group>

:::

:::details Responses

- 200 OK

  - [Session](/reference/structures/errors.md#session)

- 401 Unauthorized

  - [InvalidSession](/reference/structures/errors.md#invalidsession)

- 403 Forbidden

  - [Banned](/reference/structures/errors.md#banned)

- 404 Not Found

  - [InvalidSession](/reference/structures/errors.md#invalidsession)

- 429 Too Many Requests

  - [RateLimited](/reference/structures/errors.md#ratelimited)

- 500 Internal Server Error

  - [Internal](/reference/structures/errors.md#internal)

:::

## POST /user/session

Create a new session (log in). The name of the session is controlled by the User-Agent Header, if the User-Agent cannot be parsed from a normal browser User-Agent, the entire User-Agent string will be used as the name.

:::tip No Authorization Required
This endpoint does not require authorization.
:::

:::warning Ratelimits
This endpoint uses a ratelimit that is separate from other endpoints, this endpoint may be used `1` time(s) every `1 minute`.
:::

:::danger Using Email for Login
Logging in with your email will be deprecated in the future, please use your username instead. Refer to [this](/deprecation-notices.md#emails-for-login) for more information.
:::

:::danger Field Changes
The `user` field has been renamed to `username` and the `pass` field has been renamed to `password` in the request body. Please use the new field names instead. Refer to [this](/deprecation-notices.md#post-user-session-fields) for more information.
:::

:::details Parameters

- Body

  - `username`

    - The username of the user you wish to authenticate as.

  - `password`

    - The password of the user you wish to authenticate as.

  - `rememberMe` _optional_

    - Wether or not your session should last for a day or ten years.

:::

:::details Example Request

<code-group>

<code-block title="cURL">

```sh
curl -X POST \
  -H "Content-Type: application/json" \
  -d "{\"username\":\"joe\",\"password\":\"joe\",\"rememberMe\":true}" \
  https://alekeagle.me/api/user/session
```

</code-block>

<code-block title="JS Fetch">

```js
fetch('https://alekeagle.me/api/user/session', {
  method: 'POST',
  credentials: 'include',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ username: 'joe', password: 'joe', rememberMe: true })
});
```

</code-block>

</code-group>

:::

:::details Responses

- 201 Created

  - [SuccessfulAuth](/reference/structures/errors.md#successfulauth)

- 400 Bad Request

  - [MissingFields](/reference/structures/errors.md#missingfields)

- 401 Unauthorized

  - [InvalidPassword](/reference/structures/errors.md#invalidpassword)

- 429 Too Many Requests

  - [RateLimited](/reference/structures/errors.md#ratelimited)

- 404 Not Found

  - [InvalidUser](/reference/structures/errors.md#invaliduser)

:::

## GET /user/sessions

Get a list of all sessions for the authenticated user.

:::details Example Request

<code-group>

<code-block title="cURL">

```sh
curl -X GET \
  -H "Authorization: token" \
  https://alekeagle.me/api/user/sessions
```

</code-block>

<code-block title="JS Fetch">

```js
fetch('https://alekeagle.me/api/user/session', {
  method: 'GET',
  credentials: 'include',
  headers: {
    Authorization: 'token'
  }
});
```

</code-block>

</code-group>

:::

:::details Responses

- 200 OK

  - [List](/reference/structures/data.md#list)<[Session](/reference/structures/data.md#session)>

- 401 Unauthorized

  - [InvalidSession](/reference/structures/errors.md#invalidsession)

- 403 Forbidden

  - [Banned](/reference/structures/errors.md#banned)

- 429 Too Many Requests

  - [RateLimited](/reference/structures/errors.md#ratelimited)

- 500 Internal Server Error

  - [Internal](/reference/structures/errors.md#internal)

:::

## DELETE /user/session/:id

Delete a specific session for the authenticated user.

:::details Parameters

- URL

  - `id`

    - The ID (iat) of the session you want to delete.

:::

:::details Example Request

<code-group>

<code-block title="cURL">

```sh
curl -X DELETE \
  -H "Authorization: token" \
  https://alekeagle.me/api/user/session/1234567890
```

</code-block>

<code-block title="JS Fetch">

```js
fetch('https://alekeagle.me/api/user/session/1234567890', {
  method: 'DELETE',
  credentials: 'include',
  headers: {
    Authorization: 'token'
  }
});
```

</code-block>

</code-group>

:::

:::details Responses

- 200 OK

  - [Generic](/reference/structures/successes.md#generic)

- 401 Unauthorized

  - [InvalidSession](/reference/structures/errors.md#invalidsession)

- 403 Forbidden

  - [Banned](/reference/structures/errors.md#banned)

- 404 Not Found

  - [InvalidSession](/reference/structures/errors.md#invalidsession)

- 429 Too Many Requests

  - [RateLimited](/reference/structures/errors.md#ratelimited)

- 500 Internal Server Error

  - [Internal](/reference/structures/errors.md#internal)

:::

## DELETE /user/sessions

Bulk delete multiple sessions for the authenticated user.

:::details Parameters

- Body

  - `sessions`

    - An array of session IDs that you want to delete, the API will ignore any and all invalid sessions provided in the payload.

:::

:::details Example Request

<code-group>

<code-block title="cURL">

```sh
curl -X DELETE \
  -H "Authorization: token" \
  -H "Content-Type: application/json" \
  -d "{\"sessions\":[\"sid1\",\"sid2\"]}" \
  https://alekeagle.me/api/user/sessions
```

</code-block>

<code-block title="JS Fetch">

```js
fetch('https://alekeagle.me/api/user/sessions', {
  credentials: 'include',
  method: 'DELETE',
  headers: {
    'Authorization': 'token',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ sessions: ['sid1', 'sid2'] })
});
```

</code-block>

</code-group>

:::

:::details Responses

- 200 OK

  - [BulkDelete](/reference/structures/data.md#bulkdelete)

- 400 Bad Request

  - [MissingFields](/reference/structures/errors.md#missingfields)

- 401 Unauthorized

  - [InvalidSession](/reference/structures/errors.md#invalidsession)

- 403 Forbidden

  - [Banned](/reference/structures/errors.md#banned)

- 429 Too Many Requests

  - [RateLimited](/reference/structures/errors.md#ratelimited)

- 500 Internal Server Error

  - [Internal](/reference/structures/errors.md#internal)

:::

## DELETE /user/sessions/all

Delete all sessions for the authenticated users.

:::details Parameters

- Query

  - `allButSelf` _optional_

    - Set to `true` to leave your session used to make the request valid, if `false` all sessions will be discarded. By default this is false.

:::

:::details Example Request

<code-group>

<code-block title="cURL">

```sh
curl -X DELETE \
  -H "Authorization: token" \
  https://alekeagle.me/api/user/sessions/all?allButSelf=true
```

</code-block>

<code-block title="JS Fetch">

```js
fetch('https://alekeagle.me/api/user/sessions/all?allbutSelf=true', {
  method: 'DELETE',
  credentials: 'include',
  headers: {
    Authorization: 'token'
  }
});
```

</code-block>

</code-group>

:::

:::details Responses

- 200 OK

  - [BulkDelete](/reference/structures/data.md#bulkdelete)

- 401 Unauthorized

  - [InvalidSession](/reference/structures/errors.md#invalidsession)

- 403 Forbidden

  - [Banned](/reference/structures/errors.md#banned)

- 429 Too Many Requests

  - [RateLimited](/reference/structures/errors.md#ratelimited)

- 500 Internal Server Error

  - [Internal](/reference/structures/errors.md#internal)

:::
