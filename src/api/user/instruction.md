# Instruction Management

These are endpoints that relate to interacting with setup instructions for various services.

## GET /instructions

Get a list of all setup instructions for various services.

:::details Parameters

- Query

  - `limit` _optional_

    - The number of instructions returned in the request, the default and max is 50.

  - `offset` _optional_

    - Used to paginate requests, default is no offset.

:::

:::details Example Requests

<code-group>

<code-block title="cURL">

```sh
curl -X GET \
  -H "Authorization: token" \
  https://alekeagle.me/api/instructions
```

</code-block>

<code-block title="JS Fetch">

```js
fetch('https://alekeagle.me/api/instructions', {
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

  - [List](/reference/structures/data.md#list)<[Instruction](/reference/structures/data.md#instruction)>

- 401 Unauthorized

  - [InvalidSession](/reference/structures/errors.md#invalidsession)

- 403 Forbidden

  - [Banned](/reference/structures/errors.md#banned)

- 429 Too Many Requests

  - [RateLimited](/reference/structures/errors.md#ratelimited)

- 500 Internal Server Error

  - [Internal](/reference/structures/errors.md#internal)

:::

## GET /instruction/:id

Get specific setup instructions for a service.

:::details Parameters

- Path

  - `id`

    - The ID of the instruction.

:::

:::details Example Requests

<code-group>

<code-block title="cURL">

```sh
curl -X GET \
  -H "Authorization: token" \
  https://alekeagle.me/api/instruction/joe
```

</code-block>

<code-block title="JS Fetch">

```js
fetch('https://alekeagle.me/api/instruction/joe', {
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

  - [Instruction](/reference/structures/data.md#instruction)

- 401 Unauthorized

  - [InvalidSession](/reference/structures/errors.md#invalidsession)

- 403 Forbidden

  - [Banned](/reference/structures/errors.md#banned)

- 404 Not Found

  - [InvalidInstruction](/reference/structures/errors.md#invalidinstruction)

- 429 Too Many Requests

  - [RateLimited](/reference/structures/errors.md#ratelimited)

- 500 Internal Server Error

  - [Internal](/reference/structures/errors.md#internal)

:::
