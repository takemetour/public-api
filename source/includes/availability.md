# Availability

## Local Experiences Trip Calendar

> Code

```shell
curl 'https://api.staging.takemetour.com/partner/calendar?trip_id=58ff211702b3ea0011efe846&month=August%202018' \
-H 'content-type: application/json' \
-H 'x-access-token: 0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/calendar?trip_id=58ff211702b3ea0011efe846&month=August%202018',
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
  "date": "2018-08-01T17:00:00.000Z",
  "status": "n/a"
}, {
  "date": "2018-08-02T17:00:00.000Z",
  "status": "n/a"
}, {
  "date": "2018-08-06T17:00:00.000Z",
  "status": "available"
}, {
  "date": "2018-08-08T17:00:00.000Z",
  "status": "n/a"
}, {
  "date": "2018-08-09T17:00:00.000Z",
  "status": "n/a"
}, {
  "date": "2018-08-13T17:00:00.000Z",
  "status": "available"
}, {
  "date": "2018-08-15T17:00:00.000Z",
  "status": "n/a"
}, {
  "date": "2018-08-16T17:00:00.000Z",
  "status": "n/a"
}, {
  "date": "2018-08-17T17:00:00.000Z",
  "status": "n/a"
}, {
  "date": "2018-08-20T17:00:00.000Z",
  "status": "available"
}, {
  "date": "2018-08-22T17:00:00.000Z",
  "status": "n/a"
}, {
  "date": "2018-08-23T17:00:00.000Z",
  "status": "n/a"
}, {
  "date": "2018-08-25T17:00:00.000Z",
  "status": "n/a"
}, {
  "date": "2018-08-27T17:00:00.000Z",
  "status": "available"
}, {
  "date": "2018-08-29T17:00:00.000Z",
  "status": "n/a"
}, {
  "date": "2018-08-30T17:00:00.000Z",
  "status": "n/a"
}]
```

**HTTP Request:** `GET /calendar?trip_id=tripId&month=monthYear`

### Request Query String

Parameter | Type | Description
--------- | ---- | -----------
trip_id | **String** | Product's database ID get from [Get Product Detail](#get-product-detail)
month | **String** | Month and year you want to query the availability, format is full name month with a space then year in AD. **eg.** `August 2018`

### Response
The response will return an availability of days in that month in Array of Objects. Each object indicate availability status on that day.

**Note** 

* The nearest date that available to order / book is **today** in Thailand time (GMT+7). Some products need to be ordered / booked in advance, it may not available for **today** or **tomorrow**.
* For some date that doesn't an have object to indicate the availability status, it means that day has default availability which require a confirmation from Local Expert / Supplyer.

For each object will have these parameters.

Parameter | Type | Description
--------- | ---- | -----------
date | **String** | Date in ISO string (at 00:00)
status | **String** | Availability status on that day. `n/a` means not available to order / book. `available` means available to order / book with an instant confirmation.

This is an example of Date Picker that we use on our system.

![Image of TakeMeTour Date Picker](https://raw.githubusercontent.com/takemetour/public-api/master/material/calendar.png)

## Attraction Tickets Calendar

> Code

```shell
curl 'https://api.staging.takemetour.com/partner/calendar?trip_id=5a14fccc8d185a001220006d&ticket_ids=4136,4137&month=August%202018' \
-H 'content-type: application/json' \
-H 'x-access-token: 0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/calendar?trip_id=5a14fccc8d185a001220006d&ticket_ids=4136,4137&month=August%202018',
{
  headers: {
    'content-type': 'application/json',
    'x-access-token': '0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3'
  },
  method: 'GET',
});
const data = await response.json();
```
**HTTP Request:** `GET /calendar?trip_id=tripId&month=monthYear&ticket_ids=ticketIds`

Some subtiers of ticket have different availability from product parent.(some required seat confirmation). If it has, you will see field `has_availability` in `multi_tier_prices[index].sub_tiers[index]` is `true`. You have to pass `globaltix_ticket_id` where you can find it in `multi_tier_prices[index].sub_tiers[index]` with the query string of the request.

As you can book multiple subtier tickets in the same tier at once (**eg.** book 2 Show + Food Adult tickets + 1 Show + Food Child ticket). You can query availabilities by passing ticket ids separated by commas (**eg.** ticket_ids=4136,4137)

### Request Query String

Parameter | Type | Description
--------- | ---- | -----------
trip_id | **String** | Product's database ID get from [Get Product Detail](#get-product-detail)
ticket_ids | **String** | `globaltix_ticket_id` in `multi_tier_prices[index].sub_tiers[index]`
month | **String** | Month and year you want to query the availability, format is full name month with a space then year in AD. **eg.** `August 2018`

### Response
The response is similar to the response of [Local Experience Trips Availability](#local-experiences-trip-calendar)

## Tangible Product Calendar

Same as [Local Experiences Trip Calendar](local-experiences-trip-calendar)
