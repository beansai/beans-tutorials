

<img src="../../assets/images/beans-128x128.png" align="right" />

# What-if with multiple day stops

We can use `include_multi_day_window_stops` to deceide whether or not to use the stops from the requests which deliver from/by is not within 24 hours

For example, if we have a stop
- 2022-04-12 10:30 (deliver_from_str)
- 2022-04-13 13:30 (deliver_by_str)

then, this stop will NOT be included when `include_multi_day_window_stops` is `false`.

## Table of contents
- [Run What If](#run-what-if)
- [Some Important Notes](#some-important-notes)

### Run What If
**Request Example - Include Stop**

Let's see how to include a stop which has a gap more than 24 hours with deliver from/by.

```
POST {{baseURL}}/enterprise/v1/lists/route_whatif
```


```json
{
    "item": [
        {
            "list_item_id": "7d4b65f1-985c-40d9-a49a-fd92be45d035-013",
            "address": "1750 Vine St, Los Angeles, CA 90028, United States",
            "deliver_from_str": "2022-04-12 15:00",
            "deliver_by_str": "2030-01-16 20:00"
        }
    ],
    "listRouteIds": [
        "40694ba8-3404-402f-a9da-d90bc22da01b"
    ],
    "include_multi_day_window_stops":true
}
```
- `include_open_stops_outside_current_date` - (optional, boolean)
  - Default is false
  - If false, it would remove the stops from request (and not from route) where the gap between deliver_from and deliver_by is more than 24 hours.
  - If true, stops from the request would be included in the route computation, and the system would currently attempt to honor that stop within the single day.

**Response Example - Include Stop**

```json
{
    "item": [
        {
            "listItemId": "7d4b65f1-985c-40d9-a49a-fd92be45d035-013",
            "address": "1750 Vine St, Los Angeles, CA 90028, United States",
            "deliverFromStr": "2022-04-12 15:00",
            "deliverByStr": "2030-01-16 20:00"
        }
    ],
    "listRouteIds": [
        "40694ba8-3404-402f-a9da-d90bc22da01b"
    ],
    "requestId": "cdb1161c8a894dcaa21cf8ea521fb035",
    "includeMultiDayWindowStops": true,
    "logs": [
        "Starting to compute what-ifs for 1 routes",
        "There are 1 routes where 0 are not suitable and 1 are possibilities"
    ],
    "status": "completed",
    "result": {
        "routes": [
            {
                "listRouteId": "40694ba8-3404-402f-a9da-d90bc22da01b",
                "deltaDistanceM": 10807.800000000017,
                "deltaTimeS": 935.8000000000029
            }
        ]
    },
    "message": "Completed"
}
```

**Request Example - Exclude Stop**
And here's how not to include it from the request.

```json
{
    "item": [
        {
            "list_item_id": "7d4b65f1-985c-40d9-a49a-fd92be45d035-013",
            "address": "1750 Vine St, Los Angeles, CA 90028, United States",
            "deliver_from_str": "2022-04-12 15:00",
            "deliver_by_str": "2030-01-16 20:00"
        }
    ],
    "listRouteIds": [
        "40694ba8-3404-402f-a9da-d90bc22da01b"
    ],
    "include_multi_day_window_stops":false
}
```

**Response Example - Exclude Stop**

Since all stops from the request have been removed according to the constraint of `include_multi_day_window_stops`, there's no `deltaDistanceM` and `deltaTimeS` for the retuls.

```json
{
    "item": [
        {
            "listItemId": "7d4b65f1-985c-40d9-a49a-fd92be45d035-013",
            "address": "1750 Vine St, Los Angeles, CA 90028, United States",
            "deliverFromStr": "2022-04-12 15:00",
            "deliverByStr": "2030-01-16 20:00"
        }
    ],
    "listRouteIds": [
        "40694ba8-3404-402f-a9da-d90bc22da01b"
    ],
    "requestId": "84ad2749decb491b9c0ce285192820ae",
    "logs": [
        "Starting to compute what-ifs for 1 routes",
        "There are 1 routes where 0 are not suitable and 1 are possibilities"
    ],
    "status": "completed",
    "result": {
        "routes": [
            {
                "listRouteId": "40694ba8-3404-402f-a9da-d90bc22da01b"
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