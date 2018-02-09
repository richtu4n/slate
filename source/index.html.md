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

## Retrieve a traveller

> Example Request

```javascript
const Api = require('hotelflex-client')('AUTH_TOKEN')

const traveller = Api.TravellerDirectory.Traveller.retrieve('1')
```

> Example Response

```json
{
  "id": "1",
  "email": "example@hotelflex.io",
  "profile": {}
}
```

This endpoint retrieves a specific traveller by its id.

### HTTP Request

`GET https://api.hotelflex.io/TDIR/travellers/<id>`

### URL Parameters

Parameter | Required | Description
--------- | -------- | -----------
id | true | The id of the traveller to retrieve.


## Search travellers

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
    "email": "example@hotelflex.io",
    "profile": {},
    "meta": { "reference": "TEST_REF" }
  }
]
```

This endpoint retrieves all travellers.

### HTTP Request

`GET https://api.hotelflex.io/TDIR/travellers`

### Query Parameters

Parameter | Required | Description
--------- | -------- | -----------
meta | false | The result will contain travellers whose meta field contains this object.


## Register a traveller

> Example Request

```javascript
const Api = require('hotelflex-client')('AUTH_TOKEN')

const traveller = Api.TravellerDirectory.Traveller.register({
  email: 'example@hotelflex.io',
  profile: {},
})
```

> Example Response

```json
{
  "id": "1",
  "email": "example@hotelflex.io",
  "profile": {}
},
```

This endpoint registers a new traveller.

### HTTP Request

`POST https://api.hotelflex.io/TDIR/travellers/register`

### Body Parameters

Parameter | Required | Description
--------- | -------- | -----------
email | true | This is the travellers email address.
profile | true | This is the travellers profile.
phoneNumber | false | This is the travellers phone number.
meta | false | This is an object you can put anything into.


## Update a traveller

> Example Request

```javascript
const Api = require('hotelflex-client')('AUTH_TOKEN')

const traveller = Api.TravellerDirectory.Traveller.update({
  profile: {},
  phoneNumber: "0712345689"
})
```

> Example Response

```json
{
  "id": "1",
  "email": "example@hotelflex.io",
  "profile": {}
  "phoneNumber": "0712345689",
},
```

This endpoint updates the data on the traveller.

### HTTP Request

`POST https://api.hotelflex.io/TDIR/travellers/update`

### Body Parameters

Parameter | Required | Description
--------- | -------- | -----------
id | true | This is the id of the traveller.
profile | false | This is the travellers profile.
phoneNumber | false | This is the travellers phone number.


# Hotels

## Retrieve

> Example Request

```javascript
const Api = require('hotelflex-client')('AUTH_TOKEN')

const hotel = Api.HotelManagement.Hotel.retrieve('1')
```

> Example Response

```json
{
  "id": "1",
  "name": "test hotel",
  "users": [
    {
      "id": "1",
      "accountId": "1",
      "active": true
    }
  ],
  "meta": {}
}
```

This endpoint retrieves a hotel.

### HTTP Request

`GET https://api.hotelflex.io/HM/hotels/<id>`

### URL Parameters

Parameter | Required | Description
--------- | -------- | -----------
id | true | This is the id of the hotel.


## Search

> Example Request

```javascript
const Api = require('hotelflex-client')('AUTH_TOKEN')

const hotel = Api.HotelManagement.Hotel.search({
  name: 'test hotel',
  meta: { reference: 'TEST_REF' },
})
```

> Example Response

```json
[
  {
    "id": "1",
    "name": "test hotel",
    "users": [
      {
        "id": "1",
        "accountId": "1",
        "active": true
      }
    ],
    "meta": { "reference": "TEST_REF" }
  }
]
```

This endpoint searches for hotels that match the search query.

### HTTP Request

`GET https://api.hotelflex.io/HM/hotels`

### Query Parameters

Parameter | Required | Description
--------- | -------- | -----------
name | false | This is the name of the hotel.
meta | false | The result will contain hotels whose meta field contains this object.