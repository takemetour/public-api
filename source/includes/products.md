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
	"product_type": "trip",
  "tags": [
    "tour_lx",
    "en_boating"
  ]
}
```

> Code

```shell
curl 'https://api.staging.takemetour.com/partner/products/550ae951009be2a14b193348' \
-H 'content-type: application/json' \
-H 'x-access-token: 4obGgRjmzYOnZLOEFfFsEycy04w9y8XQ'
-X GET
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/products/550ae951009be2a14b193348',
{
  headers: {
    'content-type': 'application/json',
    'x-access-token': '4obGgRjmzYOnZLOEFfFsEycy04w9y8XQ'
  },
  method: 'GET',
});
const data = await response.json();
```

**HTTP Request:** `GET /products/:slug`

### Product types

In TakeMeTour. We have 3 types of product which are

- **Local Experience Trips (`trip`)**: Our main product which is an one-day trip.
- **Attraction Tickets (`ticket`)**: Ticket for attractions location (ex. SEA LIFE Ocean World)
- **Tangible Products (`souvenir`)**

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
user_id | **User** | Owner of product
destination_location | **String** | Destination location city for this product
transportation | **String** | Transportation that support for this product
itinerary | **Array of Object** | Product itinerary, ordered by time.
meeting_points | **Array of Object** | Meeting point that provide in product. In the object has field `type` to indicate which type of meeting point is. Has 5 types `BTS Station` / `MRT Station` / `Railway Station` / `Airport` / `Hotel Pickup`
images | **Array of Object** | Images for this product with caption for each image
cover_image | **String** | Image path that use as cover image (thumbnail) for this product.
faqs | **Array of Object** | FAQs for products
tags | **Array of String** | Tags of product. See [appendix](#tag) for more detail on which tag you need to consider.
