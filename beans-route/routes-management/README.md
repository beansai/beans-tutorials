

<img src="../../assets/images/beans-128x128.png" align="right" />

# Routes Managements



For details of a route's shape please see https://www.beansroute.ai/route-api-v1.php#route-list-object


## Table of contents
- [Create Routes](#create-routes)
- [Update Route](#update-route)
- [Get Route List](#get-route-list)
- [Get Route](#get-route)

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

