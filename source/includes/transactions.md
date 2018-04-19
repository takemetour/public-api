# Transactions

## Get All Transactions

> Code

```shell
curl 'https://api.staging.takemetour.com/partner/transactions' \
-H 'content-type: application/json' \
-H 'x-access-token: 0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/transactions',
{
  headers: {
    'content-type': 'application/json',
    'x-access-token': '0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3'
  },
  method: 'GET',
});
const data = await response.json();
```

> Response

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

> Code

```shell
curl 'https://api.staging.takemetour.com/partner/transactions/5aaf7caa551d7a00116ea4fb' \
-H 'content-type: application/json' \
-H 'x-access-token: 0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/transactions/5aaf7caa551d7a00116ea4fb',
{
  headers: {
    'content-type': 'application/json',
    'x-access-token': '0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3'
  },
  method: 'GET',
});
const data = await response.json();
```

> Response

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
-H 'x-access-token: 0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3'
```
```javascript
import { saveAs } from 'file-saver'

const response = await fetch('https://api.staging.takemetour.com/partner/transactions/5aaf7caa551d7a00116ea4fb/voucher',
{
  headers: {
    'content-type': 'application/pdf',
    'x-access-token': '0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3'
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
