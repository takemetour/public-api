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
    'content-type': 'application/json',
    'x-access-token': '4obGgRjmzYOnZLOEFfFsEycy04w9y8XQ'
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
    'content-type': 'application/json',
    'x-access-token': '4obGgRjmzYOnZLOEFfFsEycy04w9y8XQ'
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
    'content-type': 'application/json',
    'x-access-token': '4obGgRjmzYOnZLOEFfFsEycy04w9y8XQ'
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
	"name": "Explore local communities of Baan Batr & Baan Nang Lerng2",
	"prices": [
		1600,
		990,
		920,
		800,
		750
	],
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
		"slug": "dang-n",
		"avatar_image": "users/rtitM-14267784330583837.jpg",
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
	"destination_location": "Bangkok",
	"transportation": "Private Car",
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
		"text": "All inclusive"
	},
	"meeting_point_locations": [
		"Bangkok",
		"Samut Prakarn",
		"Ayutthaya",
		"Hua Hin"
	],
	"images": [
		{
			"image": "trips/4uoBI-14267784502591607.jpg",
			"caption": "If you don't know what ‘Monk’s Batr’ is, I will show you the only place in Thailand that is still making it entirely by hand. I will also take you to \"Baan Nang Lerng\" an old yet classic community so that you can admire their way of life in Bangkok",
			"_id": "57277c9e6825ce9217dc82c3"
		}
	],
	"cover_image": "trips/1CTXi-1426778450712908.jpg",
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
	"product_type": "trip"
}
```
**HTTP Request:** `GET /products/:slug`

### Product types

In TakeMeTour. We have 3 types of product which are

- **Trip**: Our main product which is an one-day trip.
- **Ticket**: Ticket for attractions location (ex. SEA LIFE Ocean World)
- **Souvenir**

For this endpoint. You can identify product type via field `product_type` which can be `trip` / `ticket` / `souvenir`.

### Response

Response will be `Product` object.

Parameter | Type | Description
--------- | ---- | -----------
_id | **ObjectId** | Unique ObjectId
name | **String** | Product name
introduction | **String** | Product introduction
max_travelers | **Integer (Range 1-8 / Trip Only)** | Maximun travelers that allow for this product
slug | **String** | Product slug
user_id | **User** | Local expert for this product
destination_location | **String** | Destination location city for this product
transportation | **String** | Transportation that support for this product
itinerary | **Array of Object** | Product itinerary, ordered by time.
meeting_points | **Array of Object** | Meeting point that provide in product. In the object has field `type` to indicate which type of meeting point is. Has 5 types `BTS Station` / `MRT Station` / `Railway Station` / `Airport` / `Hotel Pickup`
images | **Array of Object** | Images for this product with caption for each image
cover_image | **String** | Image path that use as cover image (thumbnail) for this product.
faqs | **Array of Object** | FAQs for products

## Get Product Price

> Example Body for product type `trip`

```json
{
  "quantity": 2,
  "trip_id": "550ae954009be2a14b19339e"
}
```

> Example Body for product type `ticket`

```json
{
  "trip_id": "5a1e695f6ff7070010da638b",
  "multi_tier_quantity": [
    {
      "tier": "Entrance Fee with Re-entry on All Rides",
      "sub_tiers": [
        {
          "globaltix_cost": 285,
          "has_availability": false,
          "globaltix_questions": [
            {
              "id": 127761,
              "question": "Please state your date of visit",
              "type": "DATE"
            }
          ],
          "display_price": 850,
          "price": 700,
          "name": "Adult",
          "_id": "5a1e833db549a700121cb913",
          "globaltix_ticket_id": "12658",
          "globaltix_redeem": {
            "end": "2018-10-31T23:59:00",
            "start": "2017-11-16T00:00:00"
          },
          "quantity": 2
        },
        {
          "globaltix_cost": 285,
          "has_availability": false,
          "globaltix_questions": [
            {
              "id": 127761,
              "question": "Please state your date of visit",
              "type": "DATE"
            }
          ],
          "display_price": 850,
          "price": 700,
          "name": "Child",
          "_id": "5a1e833db549a700121cb912",
          "globaltix_ticket_id": "12659",
          "globaltix_redeem": {
            "end": "2018-10-31T23:59:00",
            "start": "2017-11-16T00:00:00"
          },
          "quantity": 1
        }
      ]
    },
    {
      "tier": "Entrance Fee with Re-entry on All Rides + Snow Town",
      "sub_tiers": [
        {
          "globaltix_cost": 355,
          "has_availability": false,
          "globaltix_questions": [
            {
              "id": 161384,
              "question": "Please state your date of visit.",
              "type": "DATE"
            }
          ],
          "display_price": 1030,
          "price": 820,
          "name": "Adult",
          "_id": "5a1e833db549a700121cb90d",
          "globaltix_ticket_id": "12664",
          "globaltix_redeem": {
            "end": "2018-10-31T23:59:00",
            "start": "2017-11-16T00:00:00"
          },
          "quantity": 0
        },
        {
          "globaltix_cost": 355,
          "has_availability": false,
          "globaltix_questions": [
            {
              "id": 161384,
              "question": "Please state your date of visit.",
              "type": "DATE"
            }
          ],
          "display_price": 1030,
          "price": 820,
          "name": "Child",
          "_id": "5a1e833db549a700121cb90c",
          "globaltix_ticket_id": "12665",
          "globaltix_redeem": {
            "end": "2018-10-31T23:59:00",
            "start": "2017-11-16T00:00:00"
          },
          "quantity": 0
        }
      ]
    },
    {
      "tier": "Entrance Fee with Re-entry on All Rides and Buffet Lunch",
      "sub_tiers": [
        {
          "globaltix_cost": 355,
          "has_availability": false,
          "globaltix_questions": [
            {
              "id": 161383,
              "question": "Please state your date of visit.",
              "type": "DATE"
            }
          ],
          "display_price": 1050,
          "price": 850,
          "name": "Adult",
          "_id": "5a1e833db549a700121cb910",
          "globaltix_ticket_id": "12662",
          "globaltix_redeem": {
            "end": "2018-10-31T23:59:00",
            "start": "2017-11-16T00:00:00"
          },
          "quantity": 0
        },
        {
          "globaltix_cost": 355,
          "has_availability": false,
          "globaltix_questions": [
            {
              "id": 161383,
              "question": "Please state your date of visit.",
              "type": "DATE"
            }
          ],
          "display_price": 1050,
          "price": 850,
          "name": "Child",
          "_id": "5a1e833db549a700121cb90f",
          "globaltix_ticket_id": "12663",
          "globaltix_redeem": {
            "end": "2018-10-31T23:59:00",
            "start": "2017-11-16T00:00:00"
          },
          "quantity": 0
        }
      ]
    },
    {
      "tier": "Entrance Fee with Re-entry on All Rides and Buffet Lunch + Snow Town",
      "sub_tiers": [
        {
          "globaltix_cost": 425,
          "has_availability": false,
          "globaltix_questions": [
            {
              "id": 161385,
              "question": "Please state your date of visit",
              "type": "DATE"
            }
          ],
          "display_price": 1230,
          "price": 940,
          "name": "Adult",
          "_id": "5a1e833db549a700121cb90a",
          "globaltix_ticket_id": "12666",
          "globaltix_redeem": {
            "end": "2018-10-31T23:59:00",
            "start": "2017-11-16T00:00:00"
          },
          "quantity": 0
        },
        {
          "globaltix_cost": 425,
          "has_availability": false,
          "globaltix_questions": [
            {
              "id": 161385,
              "question": "Please state your date of visit",
              "type": "DATE"
            }
          ],
          "display_price": 1130,
          "price": 940,
          "name": "Child",
          "_id": "5a1e833db549a700121cb909",
          "globaltix_ticket_id": "12667",
          "globaltix_redeem": {
            "end": "2018-10-31T23:59:00",
            "start": "2017-11-16T00:00:00"
          },
          "quantity": 0
        }
      ]
    }
  ]
}
```

> Example Response

```json
{
  "grandTotal": 1750.39,
  "partnerPricing": {
    "retailPrice": 1833.19,
    "discount": 82.8
  }
}
```

> Fetching price for trip

```shell
curl 'https://api.staging.takemetour.com/partner/price' \
-H 'content-type: application/json' \
--data-binary '{"quantity":2,"trip_id":"550ae954009be2a14b19339e"}'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/price',
{
  body: JSON.stringify({
    "quantity": 2,
    "trip_id": "550ae954009be2a14b19339e"
  }),
  headers: {
    'content-type': 'application/json'
  },
  method: 'POST',
});
const data = await response.json();
```

> Fetching price for ticket

```shell
curl 'https://api.staging.takemetour.com/partner/price' \
-H 'content-type: application/json' \
--data-binary '{"quantity":2,"trip_id":"550ae954009be2a14b19339e"}'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/price',
{
  body: JSON.stringify({
    "trip_id": "5a1e695f6ff7070010da638b",
    "multi_tier_quantity": [
      {
        "tier": "Entrance Fee with Re-entry on All Rides",
        "sub_tiers": [
          {
            "globaltix_cost": 285,
            "has_availability": false,
            "globaltix_questions": [
              {
                "id": 127761,
                "question": "Please state your date of visit",
                "type": "DATE"
              }
            ],
            "display_price": 850,
            "price": 700,
            "name": "Adult",
            "_id": "5a1e833db549a700121cb913",
            "globaltix_ticket_id": "12658",
            "globaltix_redeem": {
              "end": "2018-10-31T23:59:00",
              "start": "2017-11-16T00:00:00"
            },
            "quantity": 2
          },
          {
            "globaltix_cost": 285,
            "has_availability": false,
            "globaltix_questions": [
              {
                "id": 127761,
                "question": "Please state your date of visit",
                "type": "DATE"
              }
            ],
            "display_price": 850,
            "price": 700,
            "name": "Child",
            "_id": "5a1e833db549a700121cb912",
            "globaltix_ticket_id": "12659",
            "globaltix_redeem": {
              "end": "2018-10-31T23:59:00",
              "start": "2017-11-16T00:00:00"
            },
            "quantity": 1
          }
        ]
      },
      {
        "tier": "Entrance Fee with Re-entry on All Rides + Snow Town",
        "sub_tiers": [
          {
            "globaltix_cost": 355,
            "has_availability": false,
            "globaltix_questions": [
              {
                "id": 161384,
                "question": "Please state your date of visit.",
                "type": "DATE"
              }
            ],
            "display_price": 1030,
            "price": 820,
            "name": "Adult",
            "_id": "5a1e833db549a700121cb90d",
            "globaltix_ticket_id": "12664",
            "globaltix_redeem": {
              "end": "2018-10-31T23:59:00",
              "start": "2017-11-16T00:00:00"
            },
            "quantity": 0
          },
          {
            "globaltix_cost": 355,
            "has_availability": false,
            "globaltix_questions": [
              {
                "id": 161384,
                "question": "Please state your date of visit.",
                "type": "DATE"
              }
            ],
            "display_price": 1030,
            "price": 820,
            "name": "Child",
            "_id": "5a1e833db549a700121cb90c",
            "globaltix_ticket_id": "12665",
            "globaltix_redeem": {
              "end": "2018-10-31T23:59:00",
              "start": "2017-11-16T00:00:00"
            },
            "quantity": 0
          }
        ]
      },
      {
        "tier": "Entrance Fee with Re-entry on All Rides and Buffet Lunch",
        "sub_tiers": [
          {
            "globaltix_cost": 355,
            "has_availability": false,
            "globaltix_questions": [
              {
                "id": 161383,
                "question": "Please state your date of visit.",
                "type": "DATE"
              }
            ],
            "display_price": 1050,
            "price": 850,
            "name": "Adult",
            "_id": "5a1e833db549a700121cb910",
            "globaltix_ticket_id": "12662",
            "globaltix_redeem": {
              "end": "2018-10-31T23:59:00",
              "start": "2017-11-16T00:00:00"
            },
            "quantity": 0
          },
          {
            "globaltix_cost": 355,
            "has_availability": false,
            "globaltix_questions": [
              {
                "id": 161383,
                "question": "Please state your date of visit.",
                "type": "DATE"
              }
            ],
            "display_price": 1050,
            "price": 850,
            "name": "Child",
            "_id": "5a1e833db549a700121cb90f",
            "globaltix_ticket_id": "12663",
            "globaltix_redeem": {
              "end": "2018-10-31T23:59:00",
              "start": "2017-11-16T00:00:00"
            },
            "quantity": 0
          }
        ]
      },
      {
        "tier": "Entrance Fee with Re-entry on All Rides and Buffet Lunch + Snow Town",
        "sub_tiers": [
          {
            "globaltix_cost": 425,
            "has_availability": false,
            "globaltix_questions": [
              {
                "id": 161385,
                "question": "Please state your date of visit",
                "type": "DATE"
              }
            ],
            "display_price": 1230,
            "price": 940,
            "name": "Adult",
            "_id": "5a1e833db549a700121cb90a",
            "globaltix_ticket_id": "12666",
            "globaltix_redeem": {
              "end": "2018-10-31T23:59:00",
              "start": "2017-11-16T00:00:00"
            },
            "quantity": 0
          },
          {
            "globaltix_cost": 425,
            "has_availability": false,
            "globaltix_questions": [
              {
                "id": 161385,
                "question": "Please state your date of visit",
                "type": "DATE"
              }
            ],
            "display_price": 1130,
            "price": 940,
            "name": "Child",
            "_id": "5a1e833db549a700121cb909",
            "globaltix_ticket_id": "12667",
            "globaltix_redeem": {
              "end": "2018-10-31T23:59:00",
              "start": "2017-11-16T00:00:00"
            },
            "quantity": 0
          }
        ]
      }
    ]
  }),
  headers: {
    'content-type': 'application/json'
  },
  method: 'POST',
});
const data = await response.json();
```
**HTTP Request:** `POST /products/price`

You can get a price of product by using this API. Each type of product has a diffrent request body due to different of pricing model.

### Trip

Trip has a simplest pricing model. Price is calculated by using **quantity** and **trip_id** and API will do the rest about it.

So the request body should be

<pre class="center-column">
{
  "quantity": Number (Max at max_travelers),
  "trip_id": Trip ID (which can be found in _id of product)
}
</pre>

### Ticket

Ticket has more complicated pricing model which we called **Multi-tier pricing**

Multi-tier pricing is consist of **tier** and **sub-tier**.

To understand how multi-tier pricing model works. Let me show you an example.

In Thailand we have an amusement park called "Dream World" which sells the tickets with these 4 options to chose.

- Entrance Fee with Re-entry on All Rides
  - Adult 700 THB
  - Child 650 THB
- Entrance Fee with Re-entry on All Rides + Snow Town
  - Adult 820 THB
  - Child 770 THB
- Entrance Fee with Re-entry on All Rides + Buffet Lunch
  - Adult 850 THB
  - Child 800 THB
- Entrance Fee with Re-entry on All Rides + Snow Town + Buffet Lunch
  - Adult 940 THB
  - Child 900 THB

We called each option as **tier** so for this product we have 4 tiers. And in each tier also has sub-options called **sub-tier**. So the price of the ticket will be shown in sub-tier.

From the API that get the product details, you can get multi-tier pricing from field `multi_tier_prices` which has data structure like this

<pre class="center-column">
{
  "multi_tier_prices": [
    {
      "tier": "Entrance Fee with Re-entry on All Rides",
      "sub_tiers": [
        {
          "globaltix_cost": 285,
          "has_availability": false,
          "globaltix_questions": [
            {
              "id": 127761,
              "question": "Please state your date of visit",
              "type": "DATE"
            }
          ],
          "display_price": 850,
          "price": 700,
          "name": "Adult",
          "_id": "5a1e833db549a700121cb913",
          "globaltix_ticket_id": "12658",
          "globaltix_redeem": {
            "end": "2018-10-31T23:59:00",
            "start": "2017-11-16T00:00:00"
          }
        },
        {
          "globaltix_cost": 285,
          "has_availability": false,
          "globaltix_questions": [
            {
              "id": 127761,
              "question": "Please state your date of visit",
              "type": "DATE"
            }
          ],
          "display_price": 850,
          "price": 650,
          "name": "Child",
          "_id": "5a1e833db549a700121cb912",
          "globaltix_ticket_id": "12659",
          "globaltix_redeem": {
            "end": "2018-10-31T23:59:00",
            "start": "2017-11-16T00:00:00"
          }
        }
      ]
    },
    {
      "tier": "Entrance Fee with Re-entry on All Rides + Snow Town",
      "sub_tiers": [
        {
          "globaltix_cost": 355,
          "has_availability": false,
          "globaltix_questions": [
            {
              "id": 161384,
              "question": "Please state your date of visit.",
              "type": "DATE"
            }
          ],
          "display_price": 1030,
          "price": 820,
          "name": "Adult",
          "_id": "5a1e833db549a700121cb90d",
          "globaltix_ticket_id": "12664",
          "globaltix_redeem": {
            "end": "2018-10-31T23:59:00",
            "start": "2017-11-16T00:00:00"
          }
        },
        {
          "globaltix_cost": 355,
          "has_availability": false,
          "globaltix_questions": [
            {
              "id": 161384,
              "question": "Please state your date of visit.",
              "type": "DATE"
            }
          ],
          "display_price": 1030,
          "price": 770,
          "name": "Child",
          "_id": "5a1e833db549a700121cb90c",
          "globaltix_ticket_id": "12665",
          "globaltix_redeem": {
            "end": "2018-10-31T23:59:00",
            "start": "2017-11-16T00:00:00"
          }
        }
      ]
    },
    {
      "tier": "Entrance Fee with Re-entry on All Rides and Buffet Lunch",
      "sub_tiers": [
        {
          "globaltix_cost": 355,
          "has_availability": false,
          "globaltix_questions": [
            {
              "id": 161383,
              "question": "Please state your date of visit.",
              "type": "DATE"
            }
          ],
          "display_price": 1050,
          "price": 850,
          "name": "Adult",
          "_id": "5a1e833db549a700121cb910",
          "globaltix_ticket_id": "12662",
          "globaltix_redeem": {
            "end": "2018-10-31T23:59:00",
            "start": "2017-11-16T00:00:00"
          }
        },
        {
          "globaltix_cost": 355,
          "has_availability": false,
          "globaltix_questions": [
            {
              "id": 161383,
              "question": "Please state your date of visit.",
              "type": "DATE"
            }
          ],
          "display_price": 1050,
          "price": 800,
          "name": "Child",
          "_id": "5a1e833db549a700121cb90f",
          "globaltix_ticket_id": "12663",
          "globaltix_redeem": {
            "end": "2018-10-31T23:59:00",
            "start": "2017-11-16T00:00:00"
          }
        }
      ]
    },
    {
      "tier": "Entrance Fee with Re-entry on All Rides and Buffet Lunch + Snow Town",
      "sub_tiers": [
        {
          "globaltix_cost": 425,
          "has_availability": false,
          "globaltix_questions": [
            {
              "id": 161385,
              "question": "Please state your date of visit",
              "type": "DATE"
            }
          ],
          "display_price": 1230,
          "price": 940,
          "name": "Adult",
          "_id": "5a1e833db549a700121cb90a",
          "globaltix_ticket_id": "12666",
          "globaltix_redeem": {
            "end": "2018-10-31T23:59:00",
            "start": "2017-11-16T00:00:00"
          }
        },
        {
          "globaltix_cost": 425,
          "has_availability": false,
          "globaltix_questions": [
            {
              "id": 161385,
              "question": "Please state your date of visit",
              "type": "DATE"
            }
          ],
          "display_price": 1130,
          "price": 900,
          "name": "Child",
          "_id": "5a1e833db549a700121cb909",
          "globaltix_ticket_id": "12667",
          "globaltix_redeem": {
            "end": "2018-10-31T23:59:00",
            "start": "2017-11-16T00:00:00"
          }
        }
      ]
    }
  ]
}
</pre>

And when you want to get a price for ticket product. We just add `quantity` field in object inside `sub_tiers` array and send it to this API as field `multi_tier_quantity` (See an example on the right hand side)

**Note**

- We support only choosing single tier. So the first tier that has sub tier quantity which is not equal to 0 is consider as selected tier.
- `quantity` in sub tier is required for every tier.

### Souvenir

// Todo

### Response

Parameter | Type | Description
--------- | ---- | -----------
grandTotal | **Number** | Final price to be charged to your partner account credit.
partnerPricing | **Object** | Has sub field `retailPrice` (Original price of this product before discount) and `discount` (Discount pricing for partner)

# Transactions

## Get All transactions

> Example Response

```json
[{
  "_id": "5aa68d4dfb446d0013b8c6a0",
  "booking_number": "EYK2BJ",
  "created_at": "2018-03-12T14:23:09.161Z",
  "is_booked": true,
  // "is_canceled": false,
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
  // "is_canceled": false,
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
    'content-type': 'application/json',
    'x-access-token': '4obGgRjmzYOnZLOEFfFsEycy04w9y8XQ'
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
<!-- is_canceled | **Boolean** | Cancel status of the transaction -->
is_charged | **Boolean** | Payment status of the transaction (if it's `true` it means the payment has already been paid for this transaction)
is_confirmed | **Boolean** | Comfirmation status of the transaction (if it's `true` it means the Local Expert / Supplyer has confirmed the trip / ticket for this transaction)
price | **Object** | Pricing object
product_type | **Strig** | This value indentify the type of product. The value can be `trip` for Local Experience Trips, `ticket` for Attraction Tickets, and `souvenir` for Tangible Products (data sim, souvenir, etc.)
quantity | **Integer** | For Local Experience Trips, it is number of guest(s) who join the trip. For Tangible Product, it is number of item(s) 
trip_date | **String** | For Local Experience Trips, it is the date when trip will happen. For Tickets, it is the date when customer will enter the attraction. For Tangible Products, it is the date when product will be delivered
trip_id | **Object** | Information of product, which contains database ID, slug, and name of production
user_id | **Object** | Information of provider (Local Expert / Supplyer), which contains database ID, slug, and name of provider

## Transaction Detail

> Example Response

```json
{
  "_id": "5aaf76d7551d7a00116ea36b",
  "trip_date": "2018-04-16T17:00:00.000Z",
  "booking_number": "0MZLNH",
  "local_expert_id": {
    "_id": "5a14fccc8d185a001220006d",
    "name": {
      "first": "TakeMeTour",
      "last": "L.",
    },
    "slug": "takemetour-l"
  },
  "trip_id": {
    "_id": "5a14facc8d185a001220006d",
    "name": "Sea Life Ocean World",
    "slug": "sea-life-ocean-word"
  },
  "user_id": {
    "_id": "5a14fdcc8d185a001220006d",
    "name": {
      "first": "Demo",
      "last": "T.",
    },
    "slug": "demo-t"
  },
  "quantity": 2,
  // "is_tried_to_booked": false,
  // "is_booked_globaltix": true,
  "product_type": "ticket",
  "multi_tier_quantity": [{
    "_id": "5a5733e148838c0011058416",
    "tier": "บัตรผ่านประตูวันหยุด",
    "sub_tiers": [{
      "globaltix_cost": 270,
      "has_availability": false,
      "globaltix_questions": [{
        "id": 11969,
        "question": "Service Date",
        "type": "DATE",
        "answer": "2018-04-17"
      }, {
        "id": 11970,
        "question": "Nationality",
        "type": "FREETEXT",
        "answer": "Thai"
      }, {
        "id": 11971,
        "question": "Select Time",
        "type": "OPTION",
        "options": [
          "Afternoon",
          "Morning"
        ],
        "answer": "Morning"
      }],
      "_id": "5a5733e148838c0011058418",
      "name": "Adult",
      "price": 500,
      "quantity": 1,
      "globaltix_ticket_id": "4138",
      "display_price": 700,
      "globaltix_redeem": {
        "end": "2018-12-31T23:59:00",
        "start": "2018-01-10T00:00:00"
      }
    }, {
      "globaltix_cost": 220,
      "has_availability": false,
      "globaltix_questions": [{
        "id": 11969,
        "question": "Service Date",
        "type": "DATE",
        "answer": "2018-04-17"
      }, {
        "id": 11970,
        "question": "Nationality",
        "type": "FREETEXT",
        "answer": "Thai"
      }, {
        "id": 11971,
        "question": "Select Time",
        "type": "OPTION",
        "options": [
          "Afternoon",
          "Morning"
        ],
        "answer": "Morning"
      }],
      "_id": "5a5733e148838c0011058417",
      "name": "Child",
      "price": 300,
      "quantity": 1,
      "globaltix_ticket_id": "4139",
      "display_price": 500,
      "globaltix_redeem": {
        "end": "2018-12-31T23:59:00",
        "start": "2018-01-10T00:00:00"
      }
    }],
  }, ...],
  "is_charged": true,
  // "name": {
  //   "first": "Demo",
  //   "last": "Ticket"
  // },
  "is_instant": true,
  // "is_canceled": false,
  "is_confirmed": true,
  // "is_partner_booked": false,
  "is_booked": true,
  // "updated_at": "2018-03-19T08:37:44.363Z",
  "created_at": "2018-03-19T08:37:43.891Z",
  "price": {
    "currency": "THB",
    "perPerson": 0,
    "tax": 0,
    "discount": 0,
    "discounted": 3000,
    "grandTotal": 2800,
    "bookingFee": 0,
    "seasoned": 3000,
    "seasonedDiscountedPerPerson": 0,
    "redeemDiscount": 0,
    "displayPrice": null,
    "noRedeemPrice": 3000,
    "displaySeasonedPrice": null,
    "minimumRedeemMismatch": 0,
    "actualBookingFee": 300
  },
  // "total_lx_price": 3000,
  // "redeem": null,
  "partner_id": "5a8b9cf537308600111de430",
  "booked_at": "2018-03-19T08:37:44.131Z",
  "charged_date": "2018-03-19T08:37:44.478Z",
  // "charged_type": "partner",
  "confirmed_at": "2018-03-19T08:37:44.363Z",
}
```
> Code

```shell
curl 'https://api.staging.takemetour.com/partner/transactions/5aaf7caa551d7a00116ea4fb' \
-H 'content-type: application/json' \
-H 'x-access-token: 4obGgRjmzYOnZLOEFfFsEycy04w9y8XQ'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/transactions/5aaf7caa551d7a00116ea4fb',
{
  headers: {
    'content-type': 'application/json',
    'x-access-token': '4obGgRjmzYOnZLOEFfFsEycy04w9y8XQ'
  },
  method: 'GET',
});
const data = await response.json();
```
**HTTP Request:** `GET /transactions/:id`

### Response
The response will return transaction object

Parameter | Type | Description
--------- | ---- | -----------
_id | **ObjectId** | Transaction database ID   
booking_number | **String** | Transaction reference number 
created_at | **String** | Transaction create date and time 
is_booked | **Boolean** | Book status of the transaction
<!-- is_canceled | **Boolean** | Cancel status of the transaction -->
is_charged | **Boolean** | Payment status of the transaction (if it's `true` it means the payment has already been paid for this transaction)
is_confirmed | **Boolean** | Comfirmation status of the transaction. If it's `true` it means the Local Expert / Supplyer has confirmed the trip / ticket for this transaction. (some products on TakeMeTour have limited availability, so it need to be confirmed by Local Expert / Supplyer before complete the transaction)
is_instant | **Boolean** | Indicate the availability status of the product. If it's `true` it means the Local Expert / Supplyer will do the instant confirm once the product has been paid (Automatically comfirm by the system)
price | **Object** | Pricing object
product_type | **Strig** | This value indentify the type of product. The value can be `trip` for Local Experience Trips, `ticket` for Attraction Tickets, and `souvenir` for Tangible Products (data sim, souvenir, etc.)
quantity | **Integer** | For Local Experience Trips, it is number of guest(s) who join the trip. For Tangible Product, it is number of item(s). **For Attraction Tickets, this param will be null**
multi_tier_quantity | **Array** | For Attraction Tickets, it contains multiple tiers and subtiers of attraction ticket with detail of quantity and additional mandatory questions & answers. **For Local Experience Trips and Tangible Product, this param will be empty array**
trip_date | **String** | For Local Experience Trips, it is the date when trip will happen. For Tickets, it is the date when customer will enter the attraction. For Tangible Products, it is the date when product will be delivered
trip_id | **Object** | Information of product, which contains database ID, slug, and name of production
local_expert_id | **Object** | Information of provider (Local Expert / Supplyer), which contains database ID, slug, and name of provider
user_id | **Object** | Information of customer, which contains database ID, slug, and name of provider
booked_at | **String** | Transaction book date and time 
confirmed_at | **String** | Transaction confirm date and time 
charged_date | **String** | Transaction charge date and time 

## Voucher

> Code

```shell
curl -o voucher.pdf \
'https://api.staging.takemetour.com/partner/transactions/5aaf7caa551d7a00116ea4fb/voucher' \
-H 'x-access-token: 4obGgRjmzYOnZLOEFfFsEycy04w9y8XQ'
```
```javascript
import { saveAs } from 'file-saver'

const response = await fetch('https://api.staging.takemetour.com/partner/transactions/5aaf7caa551d7a00116ea4fb/voucher',
{
  headers: {
    'content-type': 'application/pdf',
    'x-access-token': '4obGgRjmzYOnZLOEFfFsEycy04w9y8XQ'
  },
  responseType: 'blob'
});
const blob = await response.blob();

saveAs(blob, 'voucher.pdf');
```
**HTTP Request:** `GET /transactions/:id/voucher`

### Response
The response will be PDF file **(please make sure you pass access token in header or cookie)**

Example of voucher [PDF Voucher](https://github.com/takemetour/public-api/blob/master/material/booking-voucher.pdf)
![Image of voucher](https://raw.githubusercontent.com/takemetour/public-api/master/material/booking-voucher.png)

Some Attraction Tickets voucher will look like this [PDF Ticket Voucher](https://github.com/takemetour/public-api/blob/master/material/ticket-voucher.pdf)
![Image of Attraction Tickets voucher](https://raw.githubusercontent.com/takemetour/public-api/master/material/ticket-voucher.png)

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

