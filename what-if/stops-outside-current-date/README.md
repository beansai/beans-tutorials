

<img src="../../assets/images/beans-128x128.png" align="right" />

# What-if with stops outside current date

We can use `include_open_stops_outside_current_date` to deceide whether or not to use the stops which has no intersect with current local date.

For example, if local date time of the request is 2022-03-29 and the stop has
- 2022-03-30 10:30:00 (deliver_from_str)
- 2022-03-30 13:30:00 (deliver_by_str)

then, this stop will NOT be included when `include_open_stops_outside_current_date` is `false`.

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

Let's create two routes for different date, one is today, and the other one is 2 months after.

**Request Example**

```
POST {{baseURL}}/enterprise/v1/lists/routes
```

**Body**
```json
{
    "route":[
        {
            "name": "Route June",
            "list_route_id": "June-1cf23549-0886-4b8a-be10-8fd16b8a032f",
            "status": "OPEN",
            "date_str": "2022-04-12",
            "warehouse":
            {
                "list_warehouse_id": "6f4f7bf9-b878-4eda-b01d-17dfcfcdadc3"
            }
        },
        {
            "name": "Route April",
            "list_route_id": "April-fc34ffdb-caa1-4cdb-ae15-14d3a1ac1808",
            "status": "OPEN",
            "date_str": "2031-06-13",
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
**Request Example**

Let's add stops to the routes with `deliver_from_str` and `deliver_by_str`.

Each stop will have different deliver date time.

```
POST {{baseURL}}/enterprise/v1/lists/items
```

**body**

```json
{
    "item":
    [
        {
            "listItemId": "June-1cf23549-0886-4b8a-be10-8fd16b8a032f-01",
            "address": "4531  WHITTIER BL,LOS ANGELES",
            "route":
            {
                "listRouteId": "June-1cf23549-0886-4b8a-be10-8fd16b8a032f"
            },
            "deliver_from_str": "2022-06-13 08:00",
            "deliver_by_str": "2022-06-13 09:00"
        },
        {
            "listItemId": "June-1cf23549-0886-4b8a-be10-8fd16b8a032f-02",
            "address": "18888  LABIN CT C101,ROWLAND HEIGHTS",
            "route":
            {
                "listRouteId": "June-1cf23549-0886-4b8a-be10-8fd16b8a032f"
            },
            "deliver_from_str": "2022-06-13 09:30",
            "deliver_by_str": "2022-06-13 10:00"
        },
        {
            "listItemId": "June-1cf23549-0886-4b8a-be10-8fd16b8a032f-03",
            "address": "21130  CENTRE POINTE PKWY,SANTA CLARITA",
            "route":
            {
                "listRouteId": "June-1cf23549-0886-4b8a-be10-8fd16b8a032f"
            },
            "deliver_from_str": "2022-06-13 10:30",
            "deliver_by_str": "2022-06-13 11:00"
        },
        {
            "listItemId": "April-fc34ffdb-caa1-4cdb-ae15-14d3a1ac1808-01",
            "address": "112 N GAGE AVE.,LOS ANGELES",
            "route":
            {
                "listRouteId": "April-fc34ffdb-caa1-4cdb-ae15-14d3a1ac1808"
            },
            "deliver_from_str": "2022-04-12 08:00",
            "deliver_by_str": "2022-04-12 09:00"
        },
        {
            "listItemId": "April-fc34ffdb-caa1-4cdb-ae15-14d3a1ac1808-02",
            "address": "17422  COLIMA RD,ROWLAND HEIGHTS",
            "route":
            {
                "listRouteId": "April-fc34ffdb-caa1-4cdb-ae15-14d3a1ac1808"
            },
            "deliver_from_str": "2022-04-12 09:30",
            "deliver_by_str": "2022-04-12 10:30"
        },
        {
            "listItemId": "April-fc34ffdb-caa1-4cdb-ae15-14d3a1ac1808-03",
            "address": "8115  PEARBLOSSOM HWY,LITTLEROCK",
            "route":
            {
                "listRouteId": "April-fc34ffdb-caa1-4cdb-ae15-14d3a1ac1808"
            },
            "deliver_from_str": "2022-04-12 11:00",
            "deliver_by_str": "2022-04-12 11:30"
        }
    ]
}
```

### Run What If

**Request Example**

Today is 2022-04-12, let's try to make a what-if request with empty route_id_list.

```
POST {{baseURL}}/enterprise/v1/lists/route_whatif
```

```json
{
    "item": [
        {
            "list_item_id": "7d4b65f1-985c-40d9-a49a-fd92be45d035-013",
            "address": "928 S Western Ave, Los Angeles, CA 90006, United States"
        }
    ],
    "listRouteIds": [],
    "include_open_stops_outside_current_date":false
}
```
- `include_open_stops_outside_current_date` - (optional, boolean)
  - Default is false.
  - If it is true, all the stops that are still "open" would be included in the what-if computations.
  - If it is false, then, a stop where deliver_from_str and deliver_by_str that does not intersect with the current local date time will NOT be included.

**Response Example**

From the result, we can see only stops within today has been included with calculation.

```json
{
    "item": [
        {
            "listItemId": "7d4b65f1-985c-40d9-a49a-fd92be45d035-013",
            "address": "928 S Western Ave, Los Angeles, CA 90006, United States"
        }
    ],
    "requestId": "ed823247cae8442ea5165b5fddcfa30a",
    "logs": [
        "Starting to compute what-ifs for 2 routes",
        "There are 2 routes where 1 are not suitable and 1 are possibilities"
    ],
    "status": "completed",
    "result": {
        "routes": [
            {
                "listRouteId": "April-fc34ffdb-caa1-4cdb-ae15-14d3a1ac1808",
                "deltaDistanceM": 12717.899999999994,
                "deltaTimeS": 623.2000000000007
            }
        ]
    },
    "message": "Completed"
}
```

Let's try  `include_open_stops_outside_current_date = true`

```json
{
    "item": [
        {
            "list_item_id": "7d4b65f1-985c-40d9-a49a-fd92be45d035-013",
            "address": "928 S Western Ave, Los Angeles, CA 90006, United States"
        }
    ],
    "listRouteIds": [
    ],
    "include_open_stops_outside_current_date":true
}
```

This time, we can see both stops in different date's route has been included in the calculation.
```json
{
    "item": [
        {
            "listItemId": "7d4b65f1-985c-40d9-a49a-fd92be45d035-013",
            "address": "928 S Western Ave, Los Angeles, CA 90006, United States"
        }
    ],
    "requestId": "a869510791724ddf9b90560ffde69ac2",
    "includeOpenStopsOutsideCurrentDate": true,
    "logs": [
        "Starting to compute what-ifs for 2 routes",
        "There are 2 routes where 0 are not suitable and 2 are possibilities"
    ],
    "status": "completed",
    "result": {
        "routes": [
            {
                "listRouteId": "June-1cf23549-0886-4b8a-be10-8fd16b8a032f",
                "deltaDistanceM": 2714.399999999994,
                "deltaTimeS": 397.40000000000055
            },
            {
                "listRouteId": "April-fc34ffdb-caa1-4cdb-ae15-14d3a1ac1808",
                "deltaDistanceM": 12717.899999999994,
                "deltaTimeS": 623.2000000000007
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