

<img src="../../assets/images/beans-128x128.png" align="right" />

# Stops Managements



For details of a stop (Item)  please see https://www.beansroute.ai/route-api-v1.php#item-list-object


## Table of contents
- [Create Stops](#create-stops)
- [Update Stop](#update-stop)
- [Get Stop List](#get-stop-list)
- [Get Stop](#get-stop)

### Create Stops

**Request Example**

```http
POST https://isp.beans.ai/enterprise/v1/lists/items
```

**Body**

```json
{
  "item": [
    {
      "list_item_id": "d3f6-a801b3605afbd726df743cc66",
      "address": "3365 Deer Valley Rd, Antioch, CA 94531",
      "route": {
        "list_route_id": "d3f68d55-00e7-4b7b-959d-9866c651c0eb"
      },
      "type":"PICKUP",
      "deliver_from_str":"2033-01-01 13:00",
      "deliver_by_str":"2033-01-01 18:00"
    },
    {
      "list_item_id": "d3f6-8eca53fefb635f19958ab0cbf",
      "address": "4320 E Summer Lake Dr, Oakley, CA 94561",
      "route": {
        "list_route_id": "d3f68d55-00e7-4b7b-959d-9866c651c0eb"
      },
      "type":"DROPOFF",
      "deliver_from_str":"2033-01-01 07:00",
      "deliver_by_str":"2033-01-01 11:00"
    }
  ]
}

```

**Response Example**

```
{
    "item": [
        {
            "listItemId": "d3f6-a801b3605afbd726df743cc66",
            "address": "3365 Deer Valley Rd, Antioch, CA 94531",
            "formattedAddress": "3365 Deer Valley Rd, Antioch, CA",
            "status": "NEW",
            "updatedAt": 1644400351640,
            "statusUpdatedAt": 1643267011000,
            "route": {
                "listRouteId": "d3f68d55-00e7-4b7b-959d-9866c651c0eb"
            },
            "routePriority": 6,
            "type": "PICKUP",
            "position": {
                "latitude": 37.98784,
                "longitude": -121.78451
            },
            "displayPosition": {
                "latitude": 37.98784,
                "longitude": -121.78445
            },
            "deliverFromStr": "2033-01-01 13:00",
            "deliverByStr": "2033-01-01 18:00",
            "addressComponents": {
                "zipcode": "94531",
                "countryIso3": "USA"
            }
        }
    ],
    "route": [
        {
            "listRouteId": "d3f68d55-00e7-4b7b-959d-9866c651c0eb",
            "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
            "name": "Tu Route 9d0b",
            "status": "OPEN",
            "createdAt": 1643267000000,
            "updatedAt": 1644400352000,
            "warehouse": {
                "listWarehouseId": "7bc71186-9d6f-4541-a1b3-ffcfe0b6234f",
                "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
                "address": "14840 CA-4, Discovery Bay, CA 94505",
                "formattedAddress": "14840 CA-4, Discovery Bay, CA",
                "createdAt": 1643183316000,
                "updatedAt": 1644388049000,
                "position": {
                    "latitude": 37.88946,
                    "longitude": -121.6215
                },
                "name": "Tutorial Warehouse 2"
            },
            "routePathMd5": "ea1cee82a254c506a74b6c5ec889168c",
            "dateStr": "2023-01-10",
            "startMode": "WAREHOUSE",
            "endMode": "WAREHOUSE"
        }
    ]
}
```

### Update Stop

**Request Example**

```http
POST https://isp.beans.ai/enterprise/v1/lists/items/{{list-item-id}}
```

**Body**

```
{
    "address": "3365 Deer Valley Rd, Antioch, CA 94532",
    "route": {
    "list_route_id": "d3f68d55-00e7-4b7b-959d-9866c651c0eb"
    },
    "type":"DROPOFF",
    "deliver_from_str":"2033-01-01 13:00",
    "deliver_by_str":"2033-01-01 18:00"
}
```

**Response Example**

```
{
    "item": [
        {
            "listItemId": "d3f6-a801b3605afbd726df743cc66",
            "address": "3365 Deer Valley Rd, Antioch, CA 94532",
            "formattedAddress": "3365 Deer Valley Rd, Antioch, CA",
            "status": "NEW",
            "updatedAt": 1644400495083,
            "statusUpdatedAt": 1643267011000,
            "route": {
                "listRouteId": "d3f68d55-00e7-4b7b-959d-9866c651c0eb"
            },
            "routePriority": 6,
            "type": "DROPOFF",
            "position": {
                "latitude": 37.98784,
                "longitude": -121.78451
            },
            "displayPosition": {
                "latitude": 37.98784,
                "longitude": -121.78445
            },
            "deliverFromStr": "2033-01-01 13:00",
            "deliverByStr": "2033-01-01 18:00",
            "addressComponents": {
                "zipcode": "94531",
                "countryIso3": "USA"
            }
        }
    ],
    "route": [
        {
            "listRouteId": "d3f68d55-00e7-4b7b-959d-9866c651c0eb",
            "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
            "name": "Tu Route 9d0b",
            "status": "OPEN",
            "createdAt": 1643267000000,
            "updatedAt": 1644400352000,
            "warehouse": {
                "listWarehouseId": "7bc71186-9d6f-4541-a1b3-ffcfe0b6234f",
                "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
                "address": "14840 CA-4, Discovery Bay, CA 94505",
                "formattedAddress": "14840 CA-4, Discovery Bay, CA",
                "createdAt": 1643183316000,
                "updatedAt": 1644388049000,
                "position": {
                    "latitude": 37.88946,
                    "longitude": -121.6215
                },
                "name": "Tutorial Warehouse 2"
            },
            "routePathMd5": "ea1cee82a254c506a74b6c5ec889168c",
            "dateStr": "2023-01-10",
            "startMode": "WAREHOUSE",
            "endMode": "WAREHOUSE"
        }
    ]
}
```

### Get Stop List

**Request Example**

```http
GET https://isp.beans.ai/enterprise/v1/lists/items
```

**Response**

```json
{
    "item": [
        {
            "listItemId": "d3f6-b4d913523baaee8f2ba5e1a25",
            "address": "1923 Delta Rd, Knightsen, CA 94548",
            "formattedAddress": "1923 Delta Rd, Knightsen, CA",
            "status": "NEW",
            "updatedAt": 1644400352000,
            "statusUpdatedAt": 1643267011000,
            "route": {
                "listRouteId": "d3f68d55-00e7-4b7b-959d-9866c651c0eb"
            },
            "routePriority": 4,
            "type": "DROPOFF",
            "position": {
                "latitude": 37.96883,
                "longitude": -121.6603
            },
            "displayPosition": {
                "latitude": 37.96792,
                "longitude": -121.6603
            },
            "deliverFromStr": "2033-01-01 07:00",
            "deliverByStr": "2033-01-01 11:00",
            "addressComponents": {
                "zipcode": "94548",
                "countryIso3": "USA"
            }
        }
    ]
}
```

### Get Stop

**Request Example**

```http
GET https://isp.beans.ai/enterprise/v1/lists/items/{{list-item-id}}
```

**Response Example**

```
{
    "listItemId": "d3f6-b4d913523baaee8f2ba5e1a25",
    "address": "1923 Delta Rd, Knightsen, CA 94548",
    "formattedAddress": "1923 Delta Rd, Knightsen, CA",
    "status": "NEW",
    "updatedAt": 1644400352000,
    "statusUpdatedAt": 1643267011000,
    "route": {
        "listRouteId": "d3f68d55-00e7-4b7b-959d-9866c651c0eb"
    },
    "routePriority": 4,
    "type": "DROPOFF",
    "position": {
        "latitude": 37.96883,
        "longitude": -121.6603
    },
    "displayPosition": {
        "latitude": 37.96792,
        "longitude": -121.6603
    },
    "deliverFromStr": "2033-01-01 07:00",
    "deliverByStr": "2033-01-01 11:00",
    "addressComponents": {
        "zipcode": "94548",
        "countryIso3": "USA"
    }
}
```

