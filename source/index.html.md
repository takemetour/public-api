---
title: TakeMeTour Public API

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the TakeMeTour Public API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, and Python! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/lord/slate). Feel free to edit it and use it as a base for your own API's documentation.

# API Endpoint

We provide two API endpoints for using in seperate environment.

If you are in development (or experimenting) using development endpoint.

Environment | Endpoint
---------  | -----------
Development | [https://api.staging.takemetour.com/partner](https://api.staging.takemetour.com/partner)
Production | [https://api.takemetour.com/partner](https://api.takemetour.com/partner)

# Authentication
## Login
> Example Request Body

```json
{
  "email": "demo+partner@takemetour.com",
  "password": "12345678"
}
```

> Example Response

```json
{
  "access_token": "1yOaq7O9Lcp5AKJkzMajBQ2H9gnRq2ex",
  "user": {
    "name": {
      "first": "Dang",
      "last": "Nanglerng"
    },
    "avatar_image": "users/rtitM-14267784330583837.jpg",
    "partner_credit": 50000
  }
}
```
> Code

```shell
curl 'https://api.staging.takemetour.com/partner/auth/login' \
-H 'content-type: application/json' \
--data-binary '{"email":"demo+partner@takemetour.com","password":"12345678"}'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/auth/login',
{
  body: JSON.stringify({
    email: 'demo+partner@takemetour.com',
    password: '12345678'
  }),
  headers: {
    'content-type': 'application/json'
  },
  method: 'POST',
});
const data = await response.json();
```
Request path: `/auth/login`

Request Method: `POST`

### Request Body

Parameter | Type | Description
--------- | ---- | -----------
email | **String** | partner email which registered with TakeMeTour
password | **String** | password (at least 8 characters)

### Response

Parameter | Type | Description
--------- | ---- | -----------
access_token | **String** | access token which identify user (must be added to **x-access-token** header on other request)   
user | **Object** | object of user's info 
## Logout
> Example Response

```json
{
  "success": true
}
```
> Code

```shell
curl 'https://api.staging.takemetour.com/partner/auth/logout' -X DELETE \
-H 'content-type: application/json' \
-H 'x-access-token: 4obGgRjmzYOnZLOEFfFsEycy04w9y8XQ'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/auth/logout',
{
  headers: {
    'content-type': 'application/json',
    'x-access-token': '4obGgRjmzYOnZLOEFfFsEycy04w9y8XQ'
  },
  method: 'DELETE',
});
const data = await response.json();
```
Request path: `/auth/logout`

Request Method: `DELETE`

### Response

Parameter | Type | Description
--------- | ---- | -----------
success | **Boolean** | return true   
user | **Object** | object of user's info 
## User info
> Example Response

```json
{
  "isLoggedIn": true,
  "user": {
    "name": {
      "first": "Dang",
      "last": "Nanglerng"
    },
    "avatar_image": "users/rtitM-14267784330583837.jpg",
    "partner_credit": 50000
  }
}
```
> Code

```shell
curl 'https://api.staging.takemetour.com/partner/auth/me' \
-H 'content-type: application/json' \
-H 'x-access-token: 4obGgRjmzYOnZLOEFfFsEycy04w9y8XQ'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/auth/me',
{
  headers: {
    'content-type': 'application/json'
  },
  method: 'GET',
});
const data = await response.json();
```
Request path: `/auth/me`

Request Method: `GET`

### Response

Parameter | Type | Description
--------- | ---- | -----------
isLoggedIn | **Boolean** | login status   
user | **Object** | object of user's info 

# Products

## Get All Products

> Example Response

```json
{
  "products": [Product],
  "count": 16
}
```
> Get all products with pagination via `skip` and `limit` query string

```shell
curl 'https://api.staging.takemetour.com/partner/products?city=Bangkok&skip=0&limit=10' \
-H 'content-type: application/json' \
-H 'x-access-token: 4obGgRjmzYOnZLOEFfFsEycy04w9y8XQ'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/products?skip=0&limit=10',
{
  headers: {
    'content-type': 'application/json'
  },
  method: 'GET',
});
const data = await response.json();
```
> Also support query by `product_type`

```shell
curl 'https://api.staging.takemetour.com/partner/products?city=Bangkok&product_type=trip' \
-H 'content-type: application/json' \
-H 'x-access-token: 4obGgRjmzYOnZLOEFfFsEycy04w9y8XQ'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/products?product_type=trip',
{
  headers: {
    'content-type': 'application/json'
  },
  method: 'GET',
});
const data = await response.json();
```

**Request path:** `GET /products`

**Request Method:** `GET`

### Response

Parameter | Type | Description
--------- | ---- | -----------
products | **Array of product** | login status   
count | **Integer** | All results count (without limit)

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

