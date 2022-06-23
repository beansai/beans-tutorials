

<img src="../../assets/images/beans-128x128.png" align="right" />

# Stops Management



For details of a stop (Item)  please see https://www.beansroute.ai/route-api-v1.php#item-list-object


## Table of contents
- [Create Stops](#create-stops)
- [Update Stop](#update-stop)
- [Get Stop List](#get-stop-list)
- [Get Stop](#get-stop)
- [Get all item IDs from a Route that have documentations](#get-all-item-ids-from-a-route-that-have-documentations)
- [Get Item Documentation](#get-item-documentation)
- [Search Archived Items](#search-archived-items)

### Create Stops

**Request Example**

```
POST https://isp.beans.ai/enterprise/v1/lists/items
```

**Body**
- list_item_id - ID of listItem, it is unique within the account.
- address - The address of the item.
- type - Either of DROPOFF of PICKUP
- deliver_from_str - in "yyyy-MM-dd H24:MM" format with localtime and it is interpreted to the local time as configured on the account or the route.
- deliver_to_str - in "yyyy-MM-dd H24:MM" format with localtime and it is interpreted to the local time as configured on the account or the route.
- placement - we can use this to denote the stop which size is varchar(64)

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
      "deliver_by_str":"2033-01-01 18:00",
      "placement":"T:R"
    },
    {
      "list_item_id": "d3f6-8eca53fefb635f19958ab0cbf",
      "address": "4320 E Summer Lake Dr, Oakley, CA 94561",
      "route": {
        "list_route_id": "d3f68d55-00e7-4b7b-959d-9866c651c0eb"
      },
      "type":"DROPOFF",
      "deliver_from_str":"2033-01-01 07:00",
      "deliver_by_str":"2033-01-01 11:00",
      "placement":"T:R"
    }
  ]
}

```

**Response Example**

```json
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
            },
            "placement":"T:R"
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

```
POST https://isp.beans.ai/enterprise/v1/lists/items/{{list-item-id}}
```

**Body**
- list_item_id - ID of listItem, it is unique within the account.
- address - The address of the item.
- type - Either of DROPOFF of PICKUP
- deliver_from_str - in "yyyy-MM-dd H24:MM" format with localtime and it is interpreted to the local time as configured on the account or the route.
- deliver_to_str - in "yyyy-MM-dd H24:MM" format with localtime and it is interpreted to the local time as configured on the account or the route.
- placement - we can use this to denote the stop which size is varchar(64)

```json
{
    "address": "3365 Deer Valley Rd, Antioch, CA 94532",
    "route": {
    "list_route_id": "d3f68d55-00e7-4b7b-959d-9866c651c0eb"
    },
    "type":"DROPOFF",
    "deliver_from_str":"2033-01-01 13:00",
    "deliver_by_str":"2033-01-01 18:00",
    "placement":"T:R"
}
```

**Response Example**

```json
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
            },
            "placement":"T:R"
        }
    ]
}
```

### Get Stop List

**Request Example**

```
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

```
GET https://isp.beans.ai/enterprise/v1/lists/items/{{list-item-id}}
```

**Response Example**

```json
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

### Get all item IDs from a Route that have documentations
An item is deemed to have documentation when there is a non-trivial (so, non empty) note, and a non-trivial image url.

**Request Example**
```
{{baseURL}}/enterprise/v1/lists/itemidswithdocumentation_byroute/{{route-id}}
```

**Response Example**
```json
{
    "listItemIds": [
        "ca8d-fae5d3b6b9c9f2f1a14c43b0a1"
    ]
}
```

### Get Item Documentation

Item document introduces the basic idea of contextual documentation that often 
accompany a pice of work or task. Since a piece of work/task in our ecosystem 
is currently modeled as a List Item, we are terming it Item Documentation.

For example, when a package is dropped of, the driver could ask the recipient of 
the package for signatures AND encode status of the package as part of the documentation.

**Request Example**
```
GET {{baseURL}}/enterprise/v1/lists/itemsdocumentation/{{list-item-id}}
```

**Response Example**
- image type
  - proof
  - signature
  - exception

```json
{
    "listItemId": "ca8d-fae5d3b6b9c9f2f1a14c43b0a1",
    "listRouteId": "ca8daa7f-0625-4ebe-9b57-6314e6746fef",
    "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
    "timestampEpochSecond": 1646264551,
    "notes": [
        "014-DroppedOfAtCustomer"
    ],
    "images": [
        {
            "url": "https://storage.googleapis.com/beans-images/testing/original/2022-03-02/2022-03-02_b695d615-4d32-4222-ba34-f34a68f1cee4.png",
            "type": "proof",
            "position": {
                "latitude": 20.2,
                "longitude": -30.2
            }
        }
    ],
    "eventCode": {
        "code": "014",
        "name": "DroppedOfAtCustomer"
    },
    "tags": [
        {
            "key": "/FEDEX/package_size",
            "value": "large"
        }
    ]
}
```


### Search Archived Items
**Request Example**
```
GET {{baseURL}}/enterprise/v1/lists/items/do/search?date_from=2021-01-01&date_to=2022-07-01
```
Available filters for query
- date_from - in yyyy-MM-dd format(required)
- date_to - in yyyy-MM-dd format(required)
- route_name - optional
- address - optional
- package_number - optional
- assignee_name - optional

**Response Example**
```json
{
    "item": [
        {
            "listItemId": "april-fc34ffdb-caa1-4cdb-ae15-14d3a1ac1808-01",
            "address": "112 N GAGE AVE.,LOS ANGELES",
            "formattedAddress": "112 N Gage Ave, Los Angeles, CA",
            "status": "NEW",
            "updatedAt": 1652077858000,
            "statusUpdatedAt": 1649832929000,
            "route": {
                "listRouteId": "april-fc34ffdb-caa1-4cdb-ae15-14d3a1ac1808",
                "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
                "name": "Route April",
                "status": "CLOSED",
                "createdAt": 1649832900000,
                "updatedAt": 1652077858000,
                "warehouse": {
                    "listWarehouseId": "6f4f7bf9-b878-4eda-b01d-17dfcfcdadc3",
                    "accountBuid": "4022a1aada0e4c4684e61e3f73290a68",
                    "address": "3790 Wilshire Blvd, Los Angeles, CA 90010, United States",
                    "formattedAddress": "3790 Wilshire Blvd, Los Angeles, CA",
                    "createdAt": 1649284672000,
                    "updatedAt": 1649284672000,
                    "position": {
                        "latitude": 34.06169,
                        "longitude": -118.30861
                    },
                    "name": "Thermopylae"
                },
                "routePathMd5": "1981e263541a90c2e7244d73ccc740ee",
                "dateStr": "2022-06-13",
                "startMode": "WAREHOUSE",
                "endMode": "WAREHOUSE"
            },
            "routePriority": 1,
            "type": "DROPOFF",
            "position": {
                "latitude": 34.03642,
                "longitude": -118.18464
            },
            "displayPosition": {
                "latitude": 34.03643,
                "longitude": -118.18443
            },
            "deliverFromStr": "2022-04-13 08:00",
            "deliverByStr": "2022-04-13 09:00",
            "addressComponents": {
                "city": "Los Angeles",
                "state": "CA",
                "zipcode": "90063-2306",
                "street": "112 N Gage Ave",
                "countryIso3": "USA"
            },
            "sourceSeq": 1,
            "countryIso3": "USA"
        }
    ]
}

```