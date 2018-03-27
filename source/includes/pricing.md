# Price

## Get Product Price

**HTTP Request:** `POST /products/price`

You can get a price of product by using this API. Each type of product has a diffrent request body

* [Local Experience Trips request body](#local-experience-trips-pricing-trip)
* [Attraction Tickets request body](#attraction-tickets-pricing-ticket)
* [Tangible Products request body](#tangible-products-pricing-souvenir)

due to different of pricing model. But has the **same** response body

## Local Experience Trips Pricing (`trip`)

> Example request body for product type `trip` without child price

```json
{
  "quantity": 2,
  "trip_id": "550ae954009be2a14b19339e"
}
```

> Fetching price for trip without child price

```shell
curl 'https://api.staging.takemetour.com/partner/products/price' \
-H 'content-type: application/json' \
-H 'x-access-token: 0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3' \
--data-binary '{"quantity":2,"trip_id":"550ae954009be2a14b19339e"}'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/products/price',
{
  body: JSON.stringify({
    "quantity": 2,
    "trip_id": "550ae954009be2a14b19339e"
  }),
  headers: {
    'content-type': 'application/json',
    'x-access-token': '0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3'
  },
  method: 'POST',
});
const data = await response.json();
```

> Example request body for product type `trip` with child price

```json
{
  "quantity": 2,
  "trip_id": "550ae954009be2a14b19339e",
  "selected_options": [
    {
      "lx_price": 290,
      "_id": "599e66640ea28b0011b3f147",
      "title": "Child (Age 2-12)",
      "type": "child_price",
      "price": 290,
      "quantity_type": "sum_max_travelers",
      "currency": "THB",
      "key": "children",
      "quantity": 1,
      "is_included_for_booking_fee": true
    }
  ]
}
```

> Fetching price for trip with child price

```shell
curl 'https://api.staging.takemetour.com/partner/products/price' \
-H 'content-type: application/json' \
-H 'x-access-token: 0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3' \
--data-binary '{"quantity":2,"trip_id":"550ae954009be2a14b19339e","selected_options":[{"lx_price":290,"_id":"599e66640ea28b0011b3f147","title":"Child (Age 2-12)","type":"child_price","price":290,"quantity_type":"sum_max_travelers","currency":"THB","key":"children","quantity":1,"is_included_for_booking_fee":true}]}'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/products/price',
{
  body: JSON.stringify({
    "quantity": 2,
    "trip_id": "550ae954009be2a14b19339e",
    "selected_options": [
      {
        "lx_price": 290,
        "_id": "599e66640ea28b0011b3f147",
        "title": "Child (Age 2-12)",
        "type": "child_price",
        "price": 290,
        "quantity_type": "sum_max_travelers",
        "currency": "THB",
        "key": "children",
        "quantity": 1,
        "is_included_for_booking_fee": true
      }
    ]
  }),
  headers: {
    'content-type': 'application/json',
    'x-access-token': '0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3'
  },
  method: 'POST',
});
const data = await response.json();
```

> Response

```json
{
  "grandTotal": 1750.39,
  "partnerPricing": {
    "retailPrice": 1833.19,
    "discount": 82.8
  }
}
```

### Request body

Parameter | Type | Description
--------- | ---- | -----------
quantity | **Number (Max as max_travelers)** | Quantity of traveler
trip_id | **String** | `_id` of product
selected_options | **Array of selected option** | Array of selected option which has `quantity` to specify quantity


Trip has a simplest pricing model. Price is calculated by using **quantity** and **trip_id** and API will do the rest about it.

<pre class="center-column">
{
  "quantity": 2,
  "trip_id": "550ae954009be2a14b19339e"
}
</pre>
### Child Price

Some of our trip also has **child price** which defined in `additional_options` field of product.

<pre class="center-column">
{
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
    }
  ]
}
</pre>

Child price is defined in object which has key `children`. From the above example, child price for this product is 290 THB (which is cheaper than original price)

To get a price for a trip that has child price. You must attach `selected_options` alongside with other request body (See an example at the right panel)

**Note:** Child quantity + Quantity must **not** exceed `max_travelers` (e.g. if trip has max_travelers = 5 and quantity is 3, child quantity can **not** exceed 2)

### Response

Parameter | Type | Description
--------- | ---- | -----------
grandTotal | **Number** | Final price to be charged to your partner account credit.
partnerPricing | **Object** | The object has two keys `retailPrice` (Original price of this product before discount) and `discount` (Discount pricing for partner)

## Attraction Tickets Pricing (`ticket`)

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

> Fetching price for ticket

```shell
curl 'https://api.staging.takemetour.com/partner/products/price' \
-H 'content-type: application/json' \
-H 'x-access-token: 0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3' \
--data-binary '{"trip_id":"5a3a0af6c0214700127dadf5","multi_tier_quantity":[{"tier":"Admission Fee - Aquarium Only","_id":"5a1e87a5b549a700121cb93d","sub_tiers":[{"display_price":990,"price":600,"name":"Adult","_id":"5a1e87a5b549a700121cb93f","globaltix_ticket_id":"4136","has_availability":true,"globaltix_questions":[{"type":"FREETEXT","question":"Customer name","id":11968}],"globaltix_redeem":{"end":"2018-12-31T23:59:00","start":"2018-01-10T00:00:00"},"globaltix_cost":1500,"quantity":3},{"display_price":790,"price":550,"name":"Child","_id":"5a1e87a5b549a700121cb93e","globaltix_ticket_id":"4136","has_availability":true,"globaltix_questions":[{"type":"FREETEXT","question":"Customer name","id":11968}],"globaltix_redeem":{"end":"2018-12-31T23:59:00","start":"2018-01-10T00:00:00"},"globaltix_cost":1500,"quantity":2}]},{"tier":"COMBO: Aquarium + 4D Movie","_id":"5a1e87a5b549a700121cb93a","sub_tiers":[{"display_price":1090,"price":700,"name":"Adult","_id":"5a1e87a5b549a700121cb93c","globaltix_ticket_id":"4138","has_availability":false,"globaltix_questions":[{"type":"DATE","question":"Service Date","id":11969},{"type":"FREETEXT","question":"Nationality","id":11970},{"options":["Afternoon","Morning"],"type":"OPTION","question":"Select Time","id":11971}],"globaltix_redeem":{"end":"2018-12-31T23:59:00","start":"2018-01-10T00:00:00"},"globaltix_cost":270,"quantity":0},{"display_price":890,"price":650,"name":"Child","_id":"5a1e87a5b549a700121cb93b","globaltix_ticket_id":"4139","has_availability":false,"globaltix_questions":[{"type":"DATE","question":"Service Date","id":11969},{"type":"FREETEXT","question":"Nationality","id":11970},{"options":["Afternoon","Morning"],"type":"OPTION","question":"Select Time","id":11971}],"globaltix_redeem":{"end":"2018-12-31T23:59:00","start":"2018-01-10T00:00:00"},"globaltix_cost":220,"quantity":0}]},{"tier":"Photo Pack : Aquarium + Photo (6\" x 9\")","_id":"5a1e87a5b549a700121cb937","sub_tiers":[{"display_price":1190,"price":800,"name":"Adult","_id":"5a1e87a5b549a700121cb939","quantity":0},{"display_price":990,"price":750,"name":"Child","_id":"5a1e87a5b549a700121cb938","quantity":0}]},{"tier":"Aquarium + Glass Bottom Boat (GBB)","_id":"5a1e87a5b549a700121cb934","sub_tiers":[{"display_price":1340,"price":700,"name":"Adult","_id":"5a1e87a5b549a700121cb936","quantity":0},{"display_price":1140,"price":650,"name":"Child","_id":"5a1e87a5b549a700121cb935","quantity":0}]},{"tier":"COMBI: SEA LIFE + MADAME TUSSAUDS TICKET","_id":"5a1e87a5b549a700121cb931","sub_tiers":[{"display_price":1980,"price":1000,"name":"Adult","_id":"5a1e87a5b549a700121cb933","quantity":0},{"display_price":1580,"price":850,"name":"Child","_id":"5a1e87a5b549a700121cb932","quantity":0}]}]}'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/products/price',
{
  body: JSON.stringify({
    "trip_id": "5a3a0af6c0214700127dadf5",
    "multi_tier_quantity": [
      {
        "tier": "Admission Fee - Aquarium Only",
        "_id": "5a1e87a5b549a700121cb93d",
        "sub_tiers": [
          {
            "display_price": 990,
            "price": 600,
            "name": "Adult",
            "_id": "5a1e87a5b549a700121cb93f",
            "globaltix_ticket_id": "4136",
            "has_availability": true,
            "globaltix_questions": [
              {
                "type": "FREETEXT",
                "question": "Customer name",
                "id": 11968
              }
            ],
            "globaltix_redeem": {
              "end": "2018-12-31T23:59:00",
              "start": "2018-01-10T00:00:00"
            },
            "globaltix_cost": 1500,
            "quantity": 3
          },
          {
            "display_price": 790,
            "price": 550,
            "name": "Child",
            "_id": "5a1e87a5b549a700121cb93e",
            "globaltix_ticket_id": "4136",
            "has_availability": true,
            "globaltix_questions": [
              {
                "type": "FREETEXT",
                "question": "Customer name",
                "id": 11968
              }
            ],
            "globaltix_redeem": {
              "end": "2018-12-31T23:59:00",
              "start": "2018-01-10T00:00:00"
            },
            "globaltix_cost": 1500,
            "quantity": 2
          }
        ]
      },
      {
        "tier": "COMBO: Aquarium + 4D Movie",
        "_id": "5a1e87a5b549a700121cb93a",
        "sub_tiers": [
          {
            "display_price": 1090,
            "price": 700,
            "name": "Adult",
            "_id": "5a1e87a5b549a700121cb93c",
            "globaltix_ticket_id": "4138",
            "has_availability": false,
            "globaltix_questions": [
              {
                "type": "DATE",
                "question": "Service Date",
                "id": 11969
              },
              {
                "type": "FREETEXT",
                "question": "Nationality",
                "id": 11970
              },
              {
                "options": [
                  "Afternoon",
                  "Morning"
                ],
                "type": "OPTION",
                "question": "Select Time",
                "id": 11971
              }
            ],
            "globaltix_redeem": {
              "end": "2018-12-31T23:59:00",
              "start": "2018-01-10T00:00:00"
            },
            "globaltix_cost": 270,
            "quantity": 0
          },
          {
            "display_price": 890,
            "price": 650,
            "name": "Child",
            "_id": "5a1e87a5b549a700121cb93b",
            "globaltix_ticket_id": "4139",
            "has_availability": false,
            "globaltix_questions": [
              {
                "type": "DATE",
                "question": "Service Date",
                "id": 11969
              },
              {
                "type": "FREETEXT",
                "question": "Nationality",
                "id": 11970
              },
              {
                "options": [
                  "Afternoon",
                  "Morning"
                ],
                "type": "OPTION",
                "question": "Select Time",
                "id": 11971
              }
            ],
            "globaltix_redeem": {
              "end": "2018-12-31T23:59:00",
              "start": "2018-01-10T00:00:00"
            },
            "globaltix_cost": 220,
            "quantity": 0
          }
        ]
      },
      {
        "tier": "Photo Pack : Aquarium + Photo (6\" x 9\")",
        "_id": "5a1e87a5b549a700121cb937",
        "sub_tiers": [
          {
            "display_price": 1190,
            "price": 800,
            "name": "Adult",
            "_id": "5a1e87a5b549a700121cb939",
            "quantity": 0
          },
          {
            "display_price": 990,
            "price": 750,
            "name": "Child",
            "_id": "5a1e87a5b549a700121cb938",
            "quantity": 0
          }
        ]
      },
      {
        "tier": "Aquarium + Glass Bottom Boat (GBB)",
        "_id": "5a1e87a5b549a700121cb934",
        "sub_tiers": [
          {
            "display_price": 1340,
            "price": 700,
            "name": "Adult",
            "_id": "5a1e87a5b549a700121cb936",
            "quantity": 0
          },
          {
            "display_price": 1140,
            "price": 650,
            "name": "Child",
            "_id": "5a1e87a5b549a700121cb935",
            "quantity": 0
          }
        ]
      },
      {
        "tier": "COMBI: SEA LIFE + MADAME TUSSAUDS TICKET",
        "_id": "5a1e87a5b549a700121cb931",
        "sub_tiers": [
          {
            "display_price": 1980,
            "price": 1000,
            "name": "Adult",
            "_id": "5a1e87a5b549a700121cb933",
            "quantity": 0
          },
          {
            "display_price": 1580,
            "price": 850,
            "name": "Child",
            "_id": "5a1e87a5b549a700121cb932",
            "quantity": 0
          }
        ]
      }
    ]
  }),
  headers: {
    'content-type': 'application/json',
    'x-access-token': '0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3'
  },
  method: 'POST',
});
const data = await response.json();
```

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

From the API that [get the product details](#get-product-detail), you can get multi-tier pricing from field `multi_tier_prices` which has data structure like this

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
    }
    ...
  ]
}
</pre>

And when you want to get a price for ticket product. We just add `quantity` field in object inside `sub_tiers` array and send it to this API as field `multi_tier_quantity` (See an example on the right hand side)

### Tier Schema

Parameter | Type | Description
--------- | ---- | -----------
tier | **String** | Tier name
sub_tiers | **Array of sub tier** | Array of Sub tier which has schema as shown in the next table

### Sub Tier Schema

Parameter | Type | Description
--------- | ---- | -----------
price | **Number** | Price per quantity for current sub tier
name | **String** | Sub tier name
quantity | **Number (Max to 12)** | Quantity for this sub tier

**Note**

- We support only choosing single tier. So the first tier that has sub tier quantity which is not equal to 0 is consider as selected tier.
- `quantity` in sub tier is required for every tier.

### Response
The response is similar to the response of [Local Experience Trips Pricing](#local-experience-trips-pricing-trip)

## Tangible Products Pricing (`souvenir`)

> Example body for product type `souvenir`

```json
{
  "quantity": 2,
  "trip_id": "5a3782ebbec78a00117fc04b"
}
```

> Code

```shell
curl 'https://api.staging.takemetour.com/partner/products/price' \
-H 'content-type: application/json' \
-H 'x-access-token: 0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3' \
--data-binary '{"quantity":2,"trip_id":"5a3782ebbec78a00117fc04b"}'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/products/price',
{
  body: JSON.stringify({
    "quantity": 2,
    "trip_id": "5a3782ebbec78a00117fc04b"
  }),
  headers: {
    'content-type': 'application/json',
    'x-access-token': '0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3'
  },
  method: 'POST',
});
const data = await response.json();
```

For tangible product (like data sim). The request body is the same as `trip`.

Parameter | Type | Description
--------- | ---- | -----------
quantity | **Number (Max to 12)** | Quantity of tangible product to buy
trip_id | **String** | `_id` of product

### Response
The response is similar to the response of [Local Experience Trips Pricing](#local-experience-trips-pricing-trip)