# Book

## Book Product

> Required Request body for any product type

```json
{
  "name": {
    "first": "John",
    "last": "Doe"
  },
  "email": "john+doe@takemetour.com",
  "mobile": "+66856667571",
  "country": "TH",
  "trip_id": "550ae951009be2a14b193348",
  "trip_date": "2018-04-17T17:00:00.000Z",
  "meeting_point": "BTS Station - Ari"
}
```

**HTTP Request:** `POST /book`

To book our product (a.k.a. create transaction). **There is required field for any product type** as shown below.

Parameter | Type | Description
--------- | ---- | -----------
name | **Object** | Customer first name and last name. Specific in `first` and `last` key
email | **String** | Customer email
mobile | **String** | Customer mobile (with prefix country code)
country | **String** | Country code (See [appendix](#country-code))
trip_id | **ObjectId** | `_id` of product to be book
trip_date | **ISODate string (GMT +07:00)** | Date to book the product (in case of product type `souvenir` this field is use as "delivery date" if the product is required date) in 
meeting_point | **String** | Meeting point for customer (See [appendix](#meeting-point) / Required if product has `is_hide_meeting_point` value as `false`)

**Note**

- Our API now only support payment method by using partner credit to your account.
- Make sure that your credit is sufficient for each transaction. (Checking `grandTotal` from [Get Product Price](#get-product-price) and your `partner_credit` from [User info](#user-info))

## Book Local Experience Trips

> Request body to book product type `trip`

```json
{
  "name": {
    "first": "John",
    "last": "Doe"
  },
  "email": "john+doe@takemetour.com",
  "mobile": "+66856667571",
  "country": "TH",
  "trip_id": "550ae951009be2a14b193348",
  "trip_date": "2018-04-17T17:00:00.000Z",
  "meeting_point": "BTS Station - Ari",
  "quantity": 2,
  "selected_options": [
    {
      "key": "children",
      "currency": "THB",
      "quantity_type": "sum_max_travelers",
      "price": 290,
      "type": "child_price",
      "title": "Child (Age 2-12)",
      "_id": "599e66640ea28b0011b3f147",
      "lx_price": 290,
      "is_front": false,
      "quantity": 0,
      "is_included_for_booking_fee": true
    }
  ],
}
```

> Response

```json
{
  "success": true,
  "booking_id": TransactionId
}
```

For product type `trip` you must add `quantity` and also `selected_options` for the product that has `child` key in `additional_options` field of product.

### Request body (add from [book](#book-product))

Parameter | Type | Description
--------- | ---- | -----------
quantity | **Number (limit to `max_travelers`)** | Quantity of customer
selected_options | **Array of option** | See  [child price](#child-price) for more detail

### Response
Response will return `success` to show that the booking process is success or not, and `transaction_id`.

Parameter | Type | Description
--------- | ---- | -----------
success | **Boolean** | Transaction is success or not
transaction_id | **String** | Transaction unique id
message | **String** | If transaction is not success. Message will provide

**Remark:** If `success` equal to `false` but still return `transaction_id` please contact us.

## Book Attraction Tickets

> Request body to book product type `ticket`

```json
{
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
          "quantity": 0
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
          "quantity": 0
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
              "id": 11969,
              "answer": "2018-03-30"
            },
            {
              "type": "FREETEXT",
              "question": "Nationality",
              "id": 11970,
              "answer": "Thai"
            },
            {
              "options": [
                "Afternoon",
                "Morning"
              ],
              "type": "OPTION",
              "question": "Select Time",
              "id": 11971,
              "answer": "Morning"
            }
          ],
          "globaltix_redeem": {
            "end": "2018-12-31T23:59:00",
            "start": "2018-01-10T00:00:00"
          },
          "globaltix_cost": 270,
          "quantity": 2
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
              "id": 11969,
              "answer": "2018-03-30"
            },
            {
              "type": "FREETEXT",
              "question": "Nationality",
              "id": 11970,
              "answer": "Thai"
            },
            {
              "options": [
                "Afternoon",
                "Morning"
              ],
              "type": "OPTION",
              "question": "Select Time",
              "id": 11971,
              "answer": "Morning"
            }
          ],
          "globaltix_redeem": {
            "end": "2018-12-31T23:59:00",
            "start": "2018-01-10T00:00:00"
          },
          "globaltix_cost": 220,
          "quantity": 3
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
  ],
  "name": {
    "first": "John",
    "last": "Doe"
  },
  "email": "john+doe@takemetour.com",
  "trip_date": "2018-03-29T17:00:00.000Z",
  "mobile": "+66856667571",
  "country": "TH"
}
```

> Response

```json
{
  "success": true,
  "transaction_id": TransactionId
}
```

For attraction tickets, specify `multi_tier_quantity` with the same structure as [get attraction tickets](#attraction-tickets).

But more than that, attraction ticket also has **questions** that need to be answered. Questions can be found in `globaltix_questions` in the sub tier of tier which you want to booked. (You can get it from get product API)

<pre class="center-column">
{
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
  ]
}
</pre>

The questions has 3 types that can identify via field `type`

- DATE: Answer must be date with format 'YYYY-MM-DD' (ex. 2018-02-01).
- OPTION: Answer must be one of the value in `options`. From the example, the third question has options "Afternoon" and "Morning" so answer should be one of those.
- FREETEXT: Answer can be a free text.

For example. If you want to book tier **COMBO: Aquarium + 4D Movie** you will see sub tiers of this tier. And inside each sub tier you will see `globaltix_questions`

<pre class="center-column">
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
      "quantity": 2
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
      "quantity": 3
    }
  ]
}
</pre>

Next thing you need to do is find all unique questions that unique by id. From the example, all of unique questions are these.

<pre class="center-column">
[
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
]
</pre>

So you have to answer 3 questions. The field to put answer in is `answer` inside each of question object. But you don't have to put the answer in every sub tier object. Only selected tier is required.

In an example case. We chose to book **COMBO: Aquarium + 4D Movie** tier so the answer must be provide in every sub tier as shown below. (Notice that in other tier the question still there but there is no need to answer. Even it has the same question id)

<pre class="center-column">
{
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
          "quantity": 0
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
          "quantity": 0
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
              "id": 11969,
              "answer": "2018-03-30"
            },
            {
              "type": "FREETEXT",
              "question": "Nationality",
              "id": 11970,
              "answer": "Thai"
            },
            {
              "options": [
                "Afternoon",
                "Morning"
              ],
              "type": "OPTION",
              "question": "Select Time",
              "id": 11971,
              "answer": "Morning"
            }
          ],
          "globaltix_redeem": {
            "end": "2018-12-31T23:59:00",
            "start": "2018-01-10T00:00:00"
          },
          "globaltix_cost": 270,
          "quantity": 2
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
              "id": 11969,
              "answer": "2018-03-30"
            },
            {
              "type": "FREETEXT",
              "question": "Nationality",
              "id": 11970,
              "answer": "Thai"
            },
            {
              "options": [
                "Afternoon",
                "Morning"
              ],
              "type": "OPTION",
              "question": "Select Time",
              "id": 11971,
              "answer": "Morning"
            }
          ],
          "globaltix_redeem": {
            "end": "2018-12-31T23:59:00",
            "start": "2018-01-10T00:00:00"
          },
          "globaltix_cost": 220,
          "quantity": 3
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
}
</pre>

And the above object is `multi_tier_quantity` that finally use to book.

### Request body (add from [book](#book-product))

Parameter | Type | Description
--------- | ---- | -----------
multi_tier_quantity | **Array of multi tier quantity** | Quantity of ticket with the `answer` added to the sub tier that you chose.

### Response
Response will return `success` to show that the booking process is success or not, and `transaction_id`.

Parameter | Type | Description
--------- | ---- | -----------
success | **Boolean** | Transaction is success or not
transaction_id | **String** | Transaction unique id
message | **String** | If transaction is not success. Message will provide

**Remark:** If `success` equal to `false` but still return `transaction_id` please contact us.

## Book Tangible Products

> Request body to book product type `souvenir`

```json
{
  "quantity": 1,
  "trip_id": "5a39ee73fdeeab0012005d50",
  "name": {
    "first": "John",
    "last": "Doe"
  },
  "email": "john+doe@takemetour.com",
  "trip_date": "2018-03-30T17:00:00.000Z",
  "mobile": "+66856667571",
  "country": "TH"
}
```

For tangible product, `quantity` must be provided. And it also has some condition which you need some field to add for.

- If product doesn't contain tag `not_require_pickup_location`. You must provide delivery location which is the customer's hotel (for now we will deliver the product to the customer's hotel) in the format **Hotel name: {hotelName}, room: {hotelRoom}** to the `meeting_point` field.

<pre class="center-column">
{
  "quantity": 1,
  "trip_id": "5a39ee73fdeeab0012005d50",
  "name": {
    "first": "John",
    "last": "Doe"
  },
  "email": "john+doe@takemetour.com",
  "trip_date": "2018-03-30T17:00:00.000Z",
  "mobile": "+66856667571",
  "country": "TH",
  "meeting_point": "Hotel name: Dusti Thani, room: 404"
}
</pre>

- If product contain tag `not_require_pickup_location`. Delivery location doesn't need. `meeting_point` field can be omit

- If product contain tag `match_passport_name`. You must specific name title (Mr. / Mrs. / Miss) alongside with `name.first` in request body object.

<pre class="center-column">
{
  "quantity": 1,
  "trip_id": "5a39ee73fdeeab0012005d50",
  "name": {
    "first": "Mr.John",
    "last": "Doe"
  },
  "email": "john+doe@takemetour.com",
  "trip_date": "2018-03-30T17:00:00.000Z",
  "mobile": "+66856667571",
  "country": "TH",
  "meeting_point": "Hotel name: Dusti Thani, room: 404"
}
</pre>

### Request body (add from [book](#book-product))

Parameter | Type | Description
--------- | ---- | -----------
quantity | **Number (max to 12)** | Quantity of product to be buy
meeting_point | **String** | If product `tags` doesn't contains `not_require_pickup_location` meeting_point is delivery address (hotel only).

### Response
Response will return `success` to show that the booking process is success or not, and `transaction_id`.

Parameter | Type | Description
--------- | ---- | -----------
success | **Boolean** | Transaction is success or not
transaction_id | **String** | Transaction unique id
message | **String** | If transaction is not success. Message will provide

**Remark:** If `success` equal to `false` but still return `transaction_id` please contact us.
