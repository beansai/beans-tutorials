

<img src="../../assets/images/beans-128x128.png" align="right" />

# What-if with stops outside current date

We can use `include_open_stops_outside_current_date` to deceide whether or not to use the stops from the requests which has no intersect with current local date.

For example, if local date time of the request is 2022-03-29 and the stop has
- 2022-03-28 10:30:00 (deliver_from_str)
- 2022-03-28 13:30:00 (deliver_by_str)

then, this stop will NOT be included when `include_open_stops_outside_current_date` is `false`.

## Table of contents
- [Run What If](#run-what-if)
- [Some Important Notes](#some-important-notes)


### Run What If

**Request Example**
Let's see what-if we have a stop which is far away from now.

```
POST {{baseURL}}/enterprise/v1/lists/route_whatif
```


```json
{
    "item": [
        {
            "list_item_id": "7d4b65f1-985c-40d9-a49a-fd92be45d035-013",
            "address": "1750 Vine St, Los Angeles, CA 90028, United States",
            "deliver_from_str": "2030-01-16 15:00",
            "deliver_by_str": "2030-01-17 20:00"
        }
    ],
    "listRouteIds": [
        "40694ba8-3404-402f-a9da-d90bc22da01b"
    ],
    "include_open_stops_outside_current_date":true
}
```
- `include_open_stops_outside_current_date` - (optional, boolean)
  - Default is false.
  - If it is true, all the stops that are still "open" would be included in the what-if computations.
  - If it is false, then, a stop where deliver_from_str and deliver_by_str that does not intersect with the current local date time will NOT be included.

**Response Example**

```json
{
    "item": [
        {
            "listItemId": "7d4b65f1-985c-40d9-a49a-fd92be45d035-013",
            "address": "1750 Vine St, Los Angeles, CA 90028, United States",
            "deliverFromStr": "2030-01-16 15:00",
            "deliverByStr": "2030-01-16 20:00"
        }
    ],
    "listRouteIds": [
        "40694ba8-3404-402f-a9da-d90bc22da01b"
    ],
    "requestId": "fee358f52c074436a6ff7724aa8c988f",
    "includeOpenStopsOutsideCurrentDate": true,
    "logs": [
        "Starting to compute what-ifs for 1 routes",
        "There are 1 routes where 0 are not suitable and 1 are possibilities"
    ],
    "status": "completed",
    "result": {
        "routes": [
            {
                "listRouteId": "40694ba8-3404-402f-a9da-d90bc22da01b",
                "deltaDistanceM": 34496.100000000006,
                "deltaTimeS": 1829.0
            }
        ]
    },
    "message": "Completed"
}
```

## Some Important Notes
- if a route does not have "deltaDistanceM" and "deltaTimeS", then, it is 0 (default value). This often happens when the stops to be added already exist on that route
- delta distance and time can be negative, suggesting reductions
- reduction in one DOES NOT imply reduction in another
  - for example, if a distance is reduced, but with more city driving, then, the time may be increased (sometimes quite dramatically)
- It is critical to look at both distance and time deltas to pick one that achieve proper balance. Thus, if a route has both smallest delta distance and smallest delta time, that is often a good route.
  - However, if the smallest delta distance route is not the same as the smallest delta time, it is often the case that the smallest delta time is a better route