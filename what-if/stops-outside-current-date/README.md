

<img src="../../assets/images/beans-128x128.png" align="right" />

# What-if with stops outside current date

We can use `include_open_stops_outside_current_date` to remove stops from the request which has a gap betwwen `deliver_from` and `deliver_by` is more than 24 hours.

Example,
If we have a stop
- 2022-04-13 10:30:00 (deliver_from_str)
- 2022-04-15 13:30:00 (deliver_by_str)
When we give `include_open_stops_outside_current_date = false` to the what-if request, this item would be removed from the requests since the delta time of deliver_from_str and deliver_by_str is not within 24 hours.

## Table of contents
- [Create the data](#create-the-data)
  - [Create a warehouse](#create-a-warehouse)
  - [Create routes](#create-routes)
  - [Add stops to the routes](#add-stops-to-the-routes)
- [Run What If](#run-what-if)
- [Some Important Notes](#some-important-notes)

## Create the data
### Create a warehouse

**Request Example**

```
POST {{baseURL}}/enterprise/v1/lists/warehouses
```

**Body**
- It is important to set list_warehouse_id that is unique in your account.

```json
{
  "warehouse": [
    {
      "name": "Thermopylae",
      "listWarehouseId": "d56bb78a-cdcb-4cfb-975a-597bb2b468f0",
      "address": "5905 Wilshire Blvd, Los Angeles, CA 90036, United States"
    }
  ]
}
```

**Note**: Your list_warehouse_id and address would be different.

### Create routes

A grouping Route, although isn't required for optimization, is a convenient bucket to gather
stops to be optimized.

**Request Example**

```
POST {{baseURL}}/enterprise/v1/lists/routes
```

**Body**
```json
{
    "route":[
        {
            "name": "Via Emilia",
            "list_route_id": "fa3ca41f-80fa-4b68-8315-967f0a24485f",
            "status": "OPEN",
            "date_str": "2031-02-21",
            "warehouse":
            {
                "list_warehouse_id": "6f4f7bf9-b878-4eda-b01d-17dfcfcdadc3"
            }
        }
    ]
}
```

**Note**: Your list_warehouse_id, list_route_id would be different.

### Add stops to the routes
Let's add 4 stops to the route.

**Request Example**
```
POST {{baseURL}}/enterprise/v1/lists/items
```

**body**
- Each stop contains the route reference to the route that was created above with route id.

```json
{
    "item": [
        {
            "listItemId": "adc61bbe-5d49-4d39-b298-74612296d9a9",
            "address": "31505  CASTAIC RD,CASTAIC",
            "status": "NEW",
            "route": {
                "listRouteId": "fa3ca41f-80fa-4b68-8315-967f0a24485f"
            },
            "type": "DROPOFF"
        },
        {
            "listItemId": "4e679ca6-29ae-498f-a85b-ece4a8c08851",
            "address": "25201  THE OLD RD,STEVENSON RANCH",
            "status": "NEW",
            "route": {
                "listRouteId": "fa3ca41f-80fa-4b68-8315-967f0a24485f"
            },
            "type": "DROPOFF"
        },
        {
            "listItemId": "bcc72e86-50ce-4868-87dc-ca40bc42d415",
            "address": "27911  SECO CYN RD#1A-1C,SANTA CLARITA",
            "status": "NEW",
            "route": {
                "listRouteId": "fa3ca41f-80fa-4b68-8315-967f0a24485f"
            },
            "type": "DROPOFF"
        },
        {
            "listItemId": "d01dcdf7-4f4e-4c27-a07c-8d140ad88226",
            "address": "19301  SOLEDAD CANYON,CANYON COUNTRY",
            "status": "NEW",
            "route": {
                "listRouteId": "fa3ca41f-80fa-4b68-8315-967f0a24485f"
            },
            "type": "DROPOFF"
        }
    ]
}
```


### Run What If
Now, let's see the difference of including multiple day stops or not.

**Request Example**

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
  - Default is false
  - If false, it would remove the stops from request (and not from route) where the gap between deliver_from and deliver_by is more than 24 hours. 
  - If true, such stops would be included in the route computation, and the system would currently attempt to honor that stop within the single day.

**Response Example**

```json
{
    "item": [
        {
            "listItemId": "7d4b65f1-985c-40d9-a49a-fd92be45d035-013",
            "address": "1750 Vine St, Los Angeles, CA 90028, United States",
            "deliverFromStr": "2030-01-16 15:00",
            "deliverByStr": "2030-01-17 20:00"
        }
    ],
    "listRouteIds": [
        "40694ba8-3404-402f-a9da-d90bc22da01b"
    ],
    "requestId": "e7c13d9efcc744f58ca8cb7272bcfd37",
    "includeOpenStopsOutsideCurrentDate": true,
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