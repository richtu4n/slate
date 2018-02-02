---
title: Hotelflex API Docs

search: true
---

# Introduction

This API is for internal purposes only - it is intended for other internal services to use to syncronously interact with each other.   It can be used to access all internal services and describes exactly what each endpoint does and how to call it.

# Authentication

> To authorize, use this code:

```javascript
const Api = require('hotelflex-client')('AUTH_TOKEN')
```

> Make sure to replace `AUTH_TOKEN` with the correct root token for the environment you're using.
> The development environment is configured to use 'auth_token_development'.

Hotelflex requires a root token to enable full access to the API. This token is available via the environment in all services as `process.env.ROOT_TOKEN`.

<aside class="notice">
You must replace <code>AUTH_TOKEN</code> with the root token for the environment you're working in.
</aside>

# Travellers

## Retrieve

> Example Request

```javascript
const Api = require('hotelflex-client')('AUTH_TOKEN')

const traveller = Api.TravellerDirectory.Traveller.retrieve('1')
```

> Example Response

```json
{
  "id": "1",
  "name": "John Smith"
}
```

This endpoint retrieves a specific traveller by its id.

### HTTP Request

`GET https://traveller-directory.hotelflex.io/travellers/<id>`

### URL Parameters

Parameter | Description
--------- | -----------
id | The id of the traveller to retrieve.


## Search

> Example Request

```javascript
const Api = require('hotelflex-client')('AUTH_TOKEN')

const travellers = Api.TravellerDirectory.Traveller.search({
  meta: { reference: 'TEST_REF' }
})
```

> Example Response

```json
[
  {
    "id": "1",
    "name": "John Smith"
    "meta": { "reference": "TEST_REF" }
  },
]
```

This endpoint retrieves all travellers.

### HTTP Request

`GET https://traveller-directory.hotelflex.io/travellers`

### Query Parameters

Parameter | Description
--------- | -----------
meta | The result will contain travellers whose meta field contains this object.

