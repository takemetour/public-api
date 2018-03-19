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

Welcome to the TakeMeTour Public API!

You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, and Python! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

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
--data-binary '{"email":"partner+demo@takemetour.com","password":"teamtakemetour"}'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/auth/login',
{
  body: JSON.stringify({
    email: 'partner+demo@takemetour.com',
    password: 'teamtakemetour'
  }),
  headers: {
    'content-type': 'application/json'
  },
  method: 'POST',
});
const data = await response.json();
```
**HTTP Request:** `POST /auth/login`
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
**HTTP Request:** `DELETE /auth/logout`

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
**HTTP Request:** `GET /auth/me`

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

**HTTP Request:** `GET /products`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
city | `none` | Filter by destination location city (Ex. `Bangkok` / `Chiang Mai`)
name | `none` | Search by trip name
product_type | all | Filter by product type that has 3 types allow: `trip` / `ticket` / `souvenir`
skip | 0 | Skip response results (Use for pagination)
limit | 10 | Limit response results

### Response

Parameter | Type | Description
--------- | ---- | -----------
products | **Array of product** | login status   
count | **Integer** | All results count (without limit)

For detail on Product object. See Get Product detail API below.
## Get Product detail

> Example Response

```json
{
	"_id": "550ae951009be2a14b193348",
	"duration": "6 hours",
	"introduction": "2If you don't know what ‘Monk’s Batr’ is, I will show you the only place in Thailand that is still making it entirely by hand. I will also take you to \"Baan Nang Lerng\" an old yet classic community so that you can admire their way of life in Bangkok",
	"is_flexible": false,
	"languages": [
		"English",
		"ไทย",
		"Français"
	],
	"max_travelers": 5,
	"meeting_point": {
		"hotel_area": "",
		"is_hotel": false,
		"another": {
			"name": "Landmark: Wat KhaeNangLerng"
		}
	},
	"name": "Explore local communities of Baan Batr & Baan Nang Lerng2",
	"prices": [
		1600,
		990,
		920,
		800,
		750
	],
	"rating": 3.7777777777777777,
	"seasonal_percentage": 0.15,
	"slug": "explore-local-communities-of-baan-batr-baan-nang-lerng",
	"transportations": [
		"Public transport",
		"Public Transportation"
	],
	"user_id": {
		"_id": "550ae941009be2a14b193039",
		"name": {
			"last": "N.",
			"first": "Dang"
		},
		"profile": {
			"current_city": "Bangkok Thailand",
			"about_me": "My name is Suwan Welployngam (Dang). I was born and lived in Nanglerng Community. You can call me \"Dang Nanglerng\". I'm a community leader and also community developer. This is why I have lot of knowledges about my own and nearby communities. I would like to invite you to visit my hometown, walking along a small road, meet local people and see their local lifestyle. Moreover, there's also a 100 years old house where we renovated to be public space. You can enjoy our community based activities such as Thai cooking class, Thai Dancing class and many more."
		},
		"rating": {
			"average_rating": 3.7777777777777777,
			"score": 170,
			"count": 45,
			"neutral": 11,
			"negative": 2,
			"positive": 32
		},
		"response": {
			"time": 999145.689,
			"count": 6,
			"conversation_count": 10,
			"average_time": 1353.8531848606272,
			"rate": 0.3434879155937866
		},
		"slug": "dang-n",
		"verification": {
			"bank_book_verified": true,
			"email_verified": true,
			"facebook_verified": true,
			"has_badge": true,
			"id_card_verified": false,
			"mobile_verified": true
		},
		"avatar_image": "users/rtitM-14267784330583837.jpg",
		"video_url": "",
		"available_days": [
			"default",
			"default",
			"available",
			"default",
			"n/a",
			"default",
			"default"
		]
	},
	"view_count": 5921,
	"destination_location": "Bangkok",
	"transportation": "Private Car",
	"trip_booked_count": 0,
	"conditions": [
		"physical"
	],
	"faqs": [
		{
			"answer": "If you would like to visit local communities where some traditional craftsmanships such as coffin making, bronze ware for monks, etc this trip is the one ;)",
			"question": "Why this trip?",
			"_id": "568d041e447eb1dc72e7a5ec",
			"sub": "Briefly explain your travelers why they should book your trip to quickly grasp their attentions."
		}
	],
	"intermediate_locations": [
		"Hua Hin",
		"Nakhon Pathom"
	],
	"itinerary": [
		{
			"_id": "598c24b086f80400117b9143",
			"text": "Meet up at our meeting point\n- BTS Station (Ari, Asok , Bang Chak)\n- Hotel lobby (in Bangkok area)\n- MRT Station (Bang Sue, Chatuchak Park, Hua Lamphong)\n- Railway Station (Hua Lamphong Railway Station, Hua Hin Railway Station)\n- Airport (Hua Hin Airport)",
			"time": "10:00"
		}
	],
	"meeting_points": [
		{
			"_id": "564db60c7c0732f069f1bed0",
			"city": "Bangkok",
			"type": "BTS Station",
			"name": "Ari",
			"icon_name": "bts",
			"location": {
				"lat": 13.779726,
				"lon": 100.544645
			}
		}
	],
	"price_condition": {
		"detail_traveler": [
			{
				"enabled": true,
				"text": "Meals are included. (Note that alcohol is excluded)",
				"_id": "598c24b086f80400117b9146"
			},
			{
				"enabled": true,
				"text": "Transportation fares are included.",
				"_id": "598c24b086f80400117b9145"
			},
			{
				"enabled": true,
				"text": "Admission fees are included.",
				"_id": "598c24b086f80400117b9144"
			}
		],
		"description_traveler": "<p>Transportation fares, meals, and admission fees are included. (Note that alcohol is excluded)</p>",
		"description": "<p>Expenses, occur during a trip, are mainly included</p> <p>- Public or private transportation fares : taxi, bts, mrt, etc.(Please estimate the cost of gasoline or vehicle rental fee, in case of using a private car)</p> <p>- Foods; Meal(s) during the trip. (Please note that alcohol is always excluded)</p> <p>- Admission fee: Amusement park, gallery, shows, and etc.</p>",
		"text": "All inclusive",
		"enabled_icons": [
			"food",
			"transport",
			"ticket"
		]
	},
	"meeting_point_locations": [
		"Bangkok",
		"Samut Prakarn",
		"Ayutthaya",
		"Hua Hin"
	],
	"review_count": 45,
	"search_information": {
		"is_hotel_pickup": true,
		"prices": [
			1833.19,
			1134.29,
			1054.0866666666668,
			916.595,
			859.3100000000001
		],
		"starting_time_group": "Morning",
		"duration_group": "4-6 hrs"
	},
	"available_days": [
		true,
		true,
		true,
		true,
		true,
		false,
		true
	],
	"images": [
		{
			"image": "trips/4uoBI-14267784502591607.jpg",
			"caption": "If you don't know what ‘Monk’s Batr’ is, I will show you the only place in Thailand that is still making it entirely by hand. I will also take you to \"Baan Nang Lerng\" an old yet classic community so that you can admire their way of life in Bangkok",
			"_id": "57277c9e6825ce9217dc82c3"
		}
	],
	"cover_image": "trips/1CTXi-1426778450712908.jpg",
	"video_url": "XAM0b_IV9N0",
	"is_request_form": false,
	"hours_in_advance": 24,
	"is_instant_trip": true,
	"is_unlimited_availability": true,
	"is_replaceable": false,
	"without_review_count": 78,
	"travelers_without_review": 166,
	"multi_tier_prices": [],
	"title": "",
	"attraction_location": [],
	"lx_currency": "THB",
	"additional_options": [
		{
			"lx_price": 290,
			"_id": "599e66640ea28b0011b3f147",
			"title": "Child (Age 2-12)",
			"type": "child_price",
			"price": 290,
			"quantity_type": "sum_max_travelers",
			"currency": "THB",
			"key": "children",
			"quantity": 0,
			"is_included_for_booking_fee": true
		},
		{
			"lx_price": 0,
			"key": "hotel",
			"currency": "THB",
			"quantity_type": "boolean",
			"price": 500,
			"type": "book.checkbox",
			"title": "Hotel Pickup",
			"_id": "59db3d06909883001003d38e",
			"quantity": 0,
			"is_included_for_booking_fee": true
		},
		{
			"_id": "59ddc4538463e751d6455d7a",
			"lx_price": 0,
			"key": "dtac_sim",
			"currency": "THB",
			"quantity_type": "boolean",
			"price": 199,
			"type": "book.checkbox",
			"title": "DTAC Tourist Sim",
			"quantity": 0,
			"is_included_for_booking_fee": false
		}
	],
	"product_type": "trip",
	"full_prices": [
		{
			"perPerson": 1600,
			"tax": 11.59,
			"discount": 184,
			"discounted": 1656,
			"grandTotal": 1833.19,
			"bookingFee": 165.6,
			"seasoned": 1840,
			"seasonedDiscountedPerPerson": 1656,
			"redeemDiscount": 0,
			"displayPrice": 1833.19,
			"noRedeemPrice": 1833.19,
			"displaySeasonedPrice": 2036.88,
			"minimumRedeemMismatch": 0,
			"actualBookingFee": 165.6
		}
	],
	"review_score": {
		"friendly_score": 3.2222222222222223,
		"area_score": 3.1944444444444446,
		"language_score": 3.25
	},
	"reviews": [
		{
			"_id": "5a65c67bf7b85400132bd9ae",
			"trip_id": Trip
			"local_expert_id": User,
			"user_id": User,
			"booking_id": {
				"_id": "5a40b25a7e0b5a001031bbda",
				"trip_date": "2018-01-20T17:00:00.000Z"
			},
			"score": 4,
			"text": "test",
			"header": "Good",
			"created_at": "2018-01-22T11:09:47.745Z"
		}
	]
}
```
**HTTP Request:** `GET /products/:slug`

### Response

Response will be `Product` object which has many parameter

Parameter | Type | Description
--------- | ---- | -----------
_id | **ObjectId** | Unique ObjectId
name | **String** | Product name
introduction | **String** | Product introduction
max_travelers | **Integer (Range 1-8)** | Maximun travelers that allow for this product
slug | **String** | Product slug
user_id | **User** | Local expert for this product
destination_location | **String** | Destination location city for this product
transportation | **String** | Transportation that support for this product
itinerary | **Array of Object** | Product itinerary, ordered by time.
meeting_points | **Array of Object** | Meeting point that provide in product. In the object has field `type` to indicate which type of meeting point is. Has 3 types `BTS Station` / `MRT Station` / `Railway Station` / `Airport` / `Hotel Pickup`

## Get Product Price

# Transactions

## Get All transactions

> Example Response

```json
[{
  "_id": "5aa68d4dfb446d0013b8c6a0",
  "booking_number": "EYK2BJ",
  "created_at": "2018-03-12T14:23:09.161Z",
  "is_booked": true,
  "is_canceled": false,
  "is_charged": true,
  "is_confirmed": true,
  "price": {
    "booking_fee": 100,
    "discount": 0,
    "grand_total": 1057,
    "per_person": 1000,
    "seasoned": 1000,
    "tax": 7
  },
  "product_type": "trip",
  "quantity": 1,
  "trip_date": "2018-03-25T17:00:00.000Z",
  "trip_id": {
    "_id": "58ff211702b3ea0011efe846",
    "name": "I can eat all day with the Local Farmer who's name is John1",
    "slug": "i-can-eat-all-day-with-local-farmer-who-s-name-is-john"
  },
  "user_id": {
    "_id": "5aa687e57f43ad0012b8d991",
    "name": {
      "first": "Papa",
      "last": "J."
    }
  }
},
...
{
  "_id": "5a8c073d5d27d70012d3a34f",
  "booking_number": "AKR228",
  "created_at": "2018-02-20T11:32:13.863Z",
  "is_booked": true,
  "is_canceled": false,
  "is_charged": true,
  "is_confirmed": true,
  "price": {
    "booking_fee": 0,
    "discount": 0,
    "grand_total": 600,
    "per_person": 0,
    "seasoned": 600,
    "tax": 0
  },
  "product_type": "ticket",
  "trip_date": "2018-02-21T17:00:00.000Z",
  "trip_id": {
    "_id": "5a14fccc8d185a001220006d",
    "name": "Behold the Columbia!",
    "slug": "behold-columbia"
  },
  "user_id": {
    "_id": "5a8c073d37308600111de440",
    "name": {
      "first": "John",
      "last": "N."
    }
  }
}]
```
> Code

```shell
curl 'https://api.staging.takemetour.com/partner/transactions' \
-H 'content-type: application/json' \
-H 'x-access-token: 4obGgRjmzYOnZLOEFfFsEycy04w9y8XQ'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/transactions',
{
  headers: {
    'content-type': 'application/json'
  },
  method: 'GET',
});
const data = await response.json();
```
**HTTP Request:** `GET /transactions`

### Response
The response will return an Array of Objects. For each object will have these parameters

Parameter | Type | Description
--------- | ---- | -----------
_id | **ObjectId** | Transaction database ID   
booking_number | **String** | Transaction reference number 
created_at | **String** | Transaction create date and time 
is_booked | **Boolean** | Book status of the transaction
is_canceled | **Boolean** | Cancel status of the transaction
is_charged | **Boolean** | Payment status of the transaction (if it's `true` it means the payment has already been paid for this transaction)
is_confirmed | **Boolean** | Comfirmation status of the transaction (if it's `true` it means the Local Expert / Supplyer has confirmed the trip / ticket for this transaction)
product_type | **Strig** | This value indentify the type of product. The value can be `trip` for Local Experience Trips, `ticket` for Attraction Tickets, and `souvenir` for Tangible Products (data sim, souvenir, etc.)
quantity | **Integer** | For Local Experience Trips, it is number of guest(s) who join the trip. For Tangible Product, it is number of item(s) 
trip_date | **String** | For Local Experience Trips, it is the date when trip will happen. For Tickets, it is the date when customer will enter the attraction. For Tangible Products, it is the date when product will be delivered
trip_id | **Object** | Information of product, which contains database ID, slug, and name of production
user_id | **Object** | Information of provider (Local Expert / Supplyer), which contains database ID, slug, and name of provider

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

