

<img src="../../assets/images/beans-128x128.png" align="right" />

# Route Management

For details of a route's shape please see https://www.beansroute.ai/route-api-v1.php#route-list-object


## Table of contents
- [Create Routes](#create-routes)
- [Update Route](#update-route)
- [Get Route List](#get-route-list)
- [Get Route](#get-route)
- [Delete Route](#delete-route)
- [Get Items By Route ID](#get-items-by-route-id)
- [Objects](#objects)
  - [Array of Route Object](#array-of-route-object)
  - [Route Object](#route-object)

### Create Routes

**Request Example**

```
POST https://isp.beans.ai/enterprise/v1/lists/routes
```

**Body**

- warehouse - optional to assign a route to a warehouse 
- assignee - optional to assign an assignee to the route

```json
{
    "route":
    [
        {
            "name": "Tu Route 9d0b",
            "warehouse":
            {
                "list_warehouse_id": "7bc71186-9d6f-4541-a1b3-ffcfe0b6234f"
            },
            "assignee":
            {
                "list_assignee_id": "tu1-tutorial-driver-1"
            },
            "list_route_id": "9d0b5ee9-fa02-4d6e-8633-f7980b225ae1",
            "status": "OPEN",
            "date_str": "2022-02-09"
        }
    ]
}
```

**Response Example**

```json
{
    "route": [
        {
            "listRouteId": "9d0b5ee9-fa02-4d6e-8633-f7980b225ae1",
            "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
            "name": "Tu Route 9d0b",
            "status": "OPEN",
            "assignee": {
                "listAssigneeId": "tu1-tutorial-driver-1",
                "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
                "name": "New Driver 2",
                "code": "cd787cc3-fd8",
                "createdAt": 1642408164000,
                "updatedAt": 1644388490000,
                "state": "ACTIVE",
                "role": "DRIVER",
                "employeeId": "2000001",
                "listWarehouseId": "lzt6vwxta2o0e1hsl9k75u"
            },
            "createdAt": 1643183769000,
            "updatedAt": 1644450614000,
            "warehouse": {
                "listWarehouseId": "7bc71186-9d6f-4541-a1b3-ffcfe0b6234f",
                "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
                "address": "14840 CA-4, Discovery Bay, CA 94505",
                "formattedAddress": "14840 CA-4, Discovery Bay, CA",
                "createdAt": 1643183316000,
                "updatedAt": 1644450414000,
                "position": {
                    "latitude": 37.88946,
                    "longitude": -121.6215
                },
                "name": "Tutorial Warehouse"
            },
            "routePathMd5": "4be677af73d4a8c419166ace6e707409",
            "dateStr": "2022-02-09",
            "startMode": "WAREHOUSE",
            "endMode": "WAREHOUSE",
            "tags": [
                {
                    "key": "/ROUTE/TIMEZONE",
                    "value": "America/Los_Angeles"
                }
            ]
        }
    ]
}
```

### Update Route

**Request Example**

```
POST https://isp.beans.ai/enterprise/v1/lists/routes/{{list-route-id}}
```

**Body**

- warehouse - optional to assign a route to a warehouse 
- assignee - optional to assign an assignee to the route

```json
{
    "name": "Route Name 3-1",
    "date_str": "2022-02-09",
    "status": "OPEN",
    "assignee":
    {
        "list_assignee_id": "tu1-tutorial-driver-1"
    },
    "warehouse":
    {
        "list_warehouse_id": "7bc71186-9d6f-4541-a1b3-ffcfe0b6234f"
    }
}
```

**Response Example**

```json
{
    "route": [
        {
            "listRouteId": "9d0b5ee9-fa02-4d6e-8633-f7980b225ae1",
            "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
            "name": "Tu Route 9d0b",
            "status": "OPEN",
            "createdAt": 1643183769000,
            "updatedAt": 1644386824000,
            "warehouse": {
                "listWarehouseId": "7bc71186-9d6f-4541-a1b3-ffcfe0b6234f",
                "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
                "address": "14840 CA-4, Discovery Bay, CA 94505",
                "formattedAddress": "14840 CA-4, Discovery Bay, CA",
                "createdAt": 1643183316000,
                "updatedAt": 1643183316000,
                "position": {
                    "latitude": 37.88946,
                    "longitude": -121.6215
                },
                "name": "Tutorial Warehouse"
            },
            "routePathMd5": "4be677af73d4a8c419166ace6e707409",
            "dateStr": "2023-01-10",
            "startMode": "WAREHOUSE",
            "endMode": "WAREHOUSE",
            "tags": [
                {
                    "key": "/ROUTE/TIMEZONE",
                    "value": "America/Los_Angeles"
                }
            ]
        }
    ]
}
```

### Get Route List

**Request Example**

```
GET https://isp.beans.ai/enterprise/v1/lists/routes
```

**Response Example**

```json
{
    "route": [
        {
            "listRouteId": "9d0b5ee9-fa02-4d6e-8633-f7980b225ae1",
            "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
            "name": "Tu Route 9d0b",
            "status": "OPEN",
            "createdAt": 1643183769000,
            "updatedAt": 1644386824000,
            "warehouse": {
                "listWarehouseId": "7bc71186-9d6f-4541-a1b3-ffcfe0b6234f",
                "accountBuid": "4022a1aada0e4c4684e61e3f73290a68"
            },
            "routePathMd5": "4be677af73d4a8c419166ace6e707409",
            "dateStr": "2023-01-10",
            "startMode": "WAREHOUSE",
            "endMode": "WAREHOUSE",
            "tags": [
                {
                    "key": "/ROUTE/TIMEZONE",
                    "value": "America/Los_Angeles"
                }
            ]
        }
    ]
}
```

### Get Route

**Request Example**

```
GET https://isp.beans.ai/enterprise/v1/lists/routes/{{list-route-id}}
```

**Response Example**

```json
{
    "listRouteId": "b13dfeea-d3f0-4054-91f3-aafeea458b8e",
    "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
    "name": "Tutorial Route A",
    "status": "CLOSED",
    "createdAt": 1642473157000,
    "updatedAt": 1643011733000,
    "warehouse": {
        "listWarehouseId": "cabb46d6-776a-11ec-90d6-0242ac120003",
        "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
        "address": "5655 Hood Way, Tracy, CA 95377",
        "formattedAddress": "5655 Hood Way, Tracy, CA",
        "createdAt": 1642406155000,
        "updatedAt": 1643183292000,
        "position": {
            "latitude": 37.730987,
            "longitude": -121.5088363
        }
    },
    "routePathMd5": "a819f5cb9c0b2f6af39008e99d15f124",
    "dateStr": "2023-01-10",
    "startMode": "WAREHOUSE",
    "endMode": "WAREHOUSE",
    "tags": [
        {
            "key": "/ROUTE/TIMEZONE",
            "value": "America/Los_Angeles"
        }
    ]
}
```

### Delete Route
This will perform a soft-delete action, and the deleted object will still be return in the get route by listRouteId response 
with status "CLOSED".

**Request Example**
```
DELETE {{baseURL}}/enterprise/v1/lists/items/{{list-item-id}}
```
**Response Example**
```
{
    "listRouteId": "a3cc1ed1-8586-426e-b154-e46bc7bf0c66123",
    "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
    "name": "Via Emilia a3c123",
    "status": "CLOSED",
    "createdAt": 1656546871000,
    "updatedAt": 1656546884013,
    "dateStr": "2031-02-21",
    "startMode": "WAREHOUSE",
    "endMode": "WAREHOUSE"
}
```


### Get Items By Route ID
To get non-deleted items by route id.

**Request**
```
GET {{baseURL}}/enterprise/v1/lists/routes/{{list-route-id}}/items
```

**Response Example**
```json
{
    "item": [
        {
            "listItemId": "a3cc1ed-4",
            "address": "9404 Central Ave, Montclair, CA 91763, United States",
            "formattedAddress": "9404 Central Ave, Montclair, CA",
            "status": "NEW",
            "updatedAt": 1655347418000,
            "statusUpdatedAt": 1655346404000,
            "route": {
                "listRouteId": "a3cc1ed1-8586-426e-b154-e46bc7bf0c66"
            },
            "type": "DROPOFF",
            "parentListItemId": "e20c85d1b155327a973e5fa41f0bd08d",
            "position": {
                "latitude": 34.082443,
                "longitude": -117.690918
            },
            "displayPosition": {
                "latitude": 34.082443,
                "longitude": -117.690918
            },
            "addressComponents": {
                "city": "Montclair",
                "state": "CA",
                "zipcode": "91763",
                "street": "9404 Central Ave",
                "countryIso3": "USA"
            },
            "countryIso3": "USA"
        }
        {
            "listItemId": "e20c85d1b155327a973e5fa41f0bd08d",
            "address": "9404 Central Ave, Montclair, CA",
            "notes": "Autogenerated by optimizer",
            "formattedAddress": "9404 Central Ave, Montclair, CA",
            "status": "NEW",
            "updatedAt": 1655347418000,
            "statusUpdatedAt": 1655347418000,
            "route": {
                "listRouteId": "a3cc1ed1-8586-426e-b154-e46bc7bf0c66"
            },
            "routePriority": -1,
            "trackingId": "NA, NA, NA, NA",
            "numPackages": 4,
            "type": "DROPOFF",
            "children": [
                {
                    "listItemId": "a3cc1ed-4",
                    "address": "9404 Central Ave, Montclair, CA 91763, United States",
                    "formattedAddress": "9404 Central Ave, Montclair, CA",
                    "status": "NEW",
                    "updatedAt": 1655347418000,
                    "statusUpdatedAt": 1655346404000,
                    "route": {
                        "listRouteId": "a3cc1ed1-8586-426e-b154-e46bc7bf0c66"
                    },
                    "type": "DROPOFF",
                    "parentListItemId": "e20c85d1b155327a973e5fa41f0bd08d",
                    "position": {
                        "latitude": 34.082443,
                        "longitude": -117.690918
                    },
                    "displayPosition": {
                        "latitude": 34.082443,
                        "longitude": -117.690918
                    },
                    "addressComponents": {
                        "city": "Montclair",
                        "state": "CA",
                        "zipcode": "91763",
                        "street": "9404 Central Ave",
                        "countryIso3": "USA"
                    },
                    "countryIso3": "USA"
                }
            ],
            "position": {
                "latitude": 34.082443,
                "longitude": -117.690918
            },
            "displayPosition": {
                "latitude": 34.082443,
                "longitude": -117.690918
            },
            "addressComponents": {
                "city": "Montclair",
                "state": "CA",
                "zipcode": "91763",
                "street": "9404 Central Ave",
                "countryIso3": "USA"
            },
            "sourceSeq": -1,
            "countryIso3": "USA"
        }
    ]
}
```

## Objects
### Array of Route Object
| Field | Type | Default | Description |
| --- | --- | --- | --- |
| **route** | Array of Route object | [] | A list of Route Object |

### Route Object
| Field | Type | Default | Description |
| ----------- | ----------- | ----------- | ----------- |
| **list_route_id** | string | The Route ID | The unique id of the route |
| **account_buid** | string | The account ID | The account ID that this route is in |
| **name** | string | "" | The name of the route |
| **date_str** | string | "" | The date str (yyyy-mm-dd) |
| **status** | string | "" | One of OPEN, CLOSED  |
| **manifest_name** | string | "" | The name of the manifest that was loaded to create this route |
| **assignee** | Assignee Object | {} | The Assignee object associated with this route |
| **warehouse** | Warehouse Object | {} | The warehouse object associated with this route |
| **route_path_md5** | string | "" | The md5 hash of the path last computed for this route |
| **created_at** | int64 | 0L | The timestamp, in epoch-millis, when this route is created |
| **updated_at** | int64 | 0L | The timestamp, in epoch-millis, when this route is last updated |
| **providers** | Array of string | Empty array | 0 or more providers that are associated with this route |
| **assignee_secondarys** | Array of string | Empty array | A list of assignee IDs acting as secondary assignees to this route |
| **route_type** | string | "" | One of DEFAULT, STORAGE, OMBUDSMAN or empty string to indicate the type of the route |
| **tags** | Array of Tag | Empty Array | A list of route tags. These are route preferences |
| **start_mode** | string | "" | One of WAREHOUSE, ASSIGNEE_ADDRESS, STOP, or empty string to indicate the start location of the route |
| **end_mode** | string | "" | One of WAREHOUSE, ASSIGNEE_ADDRESS, STOP, or empty string to indicate the end location of the route |

